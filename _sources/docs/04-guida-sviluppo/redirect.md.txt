## Redirect delle URI

Il presente paragrafo fornisce una guida per la creazione e la pubblicazione
dei file `htaccess` che permettono il redirect delle URI delle risorse
semantiche utilizzando il w3id.

Una volta configurati gli `htaccess` sulla base dell'organizzazione del proprio
repository contenente le risorse semantiche, sarà possibile sfruttare le URL
permanenti del w3id per referenziare le ontologie e i vocabolari.

L'efficacia delle regole di seguito descritte è subordinata all'applicazione
delle indicazioni offerte dalla presente guida per la creazione ed organizzazione
del repository contenente le risorse semantiche, con particolare riferimento 
all'uguaglianza che deve persistere tra il nome di ciascuna cartella e il nome 
dei relativi file (a meno dell'estensione) e il nome con il quale viene referenziata
la risorsa semantica (es. ontologia) all'interno della propria URI. 

### Introduzione al redirect

[w3id.org](https://w3id.org/) è una soluzione del W3C Permanent Identifier Community Group che permette l’aggiunta o modifica di identificativi permanenti a partire dai quali reindirizzare verso URL specifici; il processo si basa  sull’aggiunta di una o più cartelle nel [repository git del w3id](https://github.com/perma-id/w3id.org), le quali DEVONO contenere i file `.htaccess` e file `README.md`, eventualmente organizzati in sottocartelle.

Nel caso del Catalogo, occorre fare riferimento alla [cartella `italia` del repository git del w3id](https://github.com/perma-id/w3id.org/tree/master/italia), nella quale DEVONO essere aggiunte le sottocartelle, ciascuna per una particolare area tematica, che conterranno i file di reindirizzamento, eventualmente organizzati in ulteriori sottocartelle, ed il file `README.md`.
L’aggiunta delle sottocartelle di `'/italia'` sarà sottoposta ad approvazione del Comitato Italia; successivamente, le stesse saranno gestite autonomamente e con interfacciamento diretto verso w3id.org dai referenti indicati nei file `README.md`.
La cartella e le relative sottocartelle, i  file `.htaccess` e i file `README.md` DEVONO essere creati sul [repository git del w3id](https://github.com/perma-id/w3id.org) dall'Organizzazione contributrice.

### Processo di pubblicazione degli htaccess sul w3id

#### fork del repository GIT del w3id.org

Il primo passo per la registrazione dei vari redirect è il fork in locale della
[cartella Italia del GIT del w3id](https://github.com/perma-id/w3id.org/tree/master/italia). Gli 
identificativi permanenti (URI) verranno definiti sulla base del percorso nel quale saranno inseriti i vari file `htaccess`. Nel caso del Catalogo, il percorso della cartella “root” per nome-cartella dovrà essere 
`italia/<nome-cartella>/`, dunque il namespace degli URI definiti nella stessa sarà 
`w3id.org/italia/<nome-cartella>/`.

#### aggiunta della cartella

Nel repository in locale creato a partire dalla fork occorrerà creare la cartella `“nome-cartella”` che conterrà l’alberatura di sottocartelle e dei relativi file `.htaccess`, oltre al file `README.md`.

Di seguito è fornito un esempio di alberatura della cartella sotto `"/italia"`:

<pre>
italia
|--nome-cartella
|   |--controlled-vocabulary
|   |   |-.htaccess
|   |--data
|   |   |-.htaccess
|   |--onto
|   |   |-.htaccess
|   |README.md
</pre>

In tal modo, verranno definiti i seguenti URI:
-	`w3id.org/italia/<nome-cartella>/controlled-vocabulary`
-	`w3id.org/italia/<nome-cartella>/data`
-	`w3id.org/italia/<nome-cartella>/onto`

Il `<nome-cartella>` è molto importante dato che DEVE essere inserito in specifici parametri descritti di seguito nel presente documento, 
e sarà sempre utilizzato per riferirsi all'insieme delle risorse semantiche del Contributore nell'ambito della configurazione dei file di redirect.

Le regole di redirect associate a ciascun uri DEVONO essere definite nei relativi file `.htaccess` descritti di seguito. Il file `README.md` DEVE contenere i nominativi dei referenti unitamente ai loro riferimenti e-mail e di github. Questi riferimenti DEVONO curare la gestione della cartella e dei relativi file a seguito dell’approvazione di “Italia”. Si DOVREBBE prendere come esempio il file `README.md` sotto la cartella `"/italia"`.

#### creazione della pull request

Una volta modificato il repository GIT in locale, si DEVE creare una pull request, la quale sarà analizzata ed eventualmente validata da "Italia”; nella pull request DEVONO essere indicati come reviewer i contatti presenti nel [file README.md sotto “/italia”](https://github.com/perma-id/w3id.org/blob/master/italia/readme.md).
Il merge sul branch master verrà effettuato direttamente da w3id.org e determinerà la pubblicazione definitiva dei nuovi URI e relative regole di redirect.

### Contenuto dei file .htaccess e del README.md

Di seguito è data una descrizione di file `.htaccess` per ciascuna tipologia di risorsa, da cui l'Organizzazione contributrice DOVREBBE prendere spunto al fine creare i propri file di redirect. Gli snippet di codice di esempio sono basati sull'assunzione che per ciascuna risorsa semantica (es. ontologia) il nome della stessa nell'URI di referenziazione sia uguale al nome della cartella che contiene i relativi file sul git sorgente, e anche uguale ai nomi dei file a meno dell'estensione. In caso contrario, si renderebbe necessario sviluppare apposite regole di redirect più complesse.

#### controlled-vocabulary

Il file `.htaccess` da inserire nella sottocartella `“italia/nome-cartella/controlled-vocabulary”` DOVREBBE essere creato a prendendo come esempio [quello contenuto nella cartella del GIT “italia/controlled-vocabulary”](https://github.com/perma-id/w3id.org/blob/master/italia/controlled-vocabulary/.htaccess).

Esso contiene codice scritto sulla base delle Direttive Apache, e permette di gestire le richieste HTTP in base al valore dell'header Accept e di SYNTAX. A seconda del valore, le URL vengono riscritte in modo diverso o reindirizzate a URL esterni. La specifica azione di riscrittura o reindirizzamento dipende dalla combinazione di Accept e SYNTAX.
 
Di seguito viene data una descrizione delle direttive di esempio, alle quali DEVONO essere modificati i riferimenti degli URL di atterraggio, oltre all’eventuale modifica/integrazione delle regole al fine di meglio adattarsi al git del Contributore:

<pre>
Header set Access-Control-Allow-Origin *
</pre>
Questa riga imposta l'header Access-Control-Allow-Origin su *, consentendo a qualsiasi dominio di accedere alle risorse sul server tramite richieste Ajax o da altri domini diversi.

<pre>
Options +FollowSymLinks
</pre>
Questa riga abilita l'opzione FollowSymLinks, che permette al server di seguire i collegamenti simbolici (symlink) all'interno del file system.

<pre>
RewriteEngine on
</pre>
Questa riga attiva il motore di riscrittura delle URL di Apache (mod_rewrite), che permette di manipolare le URL delle richieste HTTP.

<pre>
SetEnvIf Accept ^.*text/turtle.* SYNTAX=ttl
SetEnvIf Accept ^.*application/json.* SYNTAX=json
SetEnvIf Accept ^.*application/csv.* SYNTAX=csv
SetEnvIf Accept ^.*text/csv.* SYNTAX=csv
SetEnvIf Accept ^.*text/html.* SYNTAX=html
</pre>
Queste righe impostano una variabile di ambiente chiamata SYNTAX in base all'header Accept della richiesta HTTP. Questo viene utilizzato per determinare il tipo di sintassi richiesto nella risposta. Queste righe DEVONO essere modificate a seconda dei formati dei file presenti nelle proprie cartelle github.

<pre>
SetEnvIf Request_URI ^.*$ ROOT_URL="url-git"
</pre>
Imposta la variabile di ambiente ROOT_URL con un URL fisso. L’URL inserito DEVE essere quello del proprio Github che punta alla cartella dei vocabolari controllati (in formato `"https://raw.githubusercontent.com/..."`)

<pre>
RewriteCond %{ENV:SYNTAX} ^(ttl|json|csv)$
RewriteRule ^([a-zA-Z-_0-9]+)(/?)$ %{ENV:ROOT_URL}$1/latest/$1.%{ENV:SYNTAX} [R=303,L]
</pre>
Definisce la regola di riscrittura dell'URL nel caso in cui il tipo file richiesto sia ttl, json o csv (questi ultimi DEVONO essere configurati sulla base dei tipi file presenti nel repository sorgente).

<pre>
RewriteCond %{ENV:SYNTAX} ^html$
RewriteRule ^(.+)$ https://schema.gov.it/lodview/"nome-cartella"/controlled-vocabulary/$1 [R=303,L]
RewriteRule ^(.+)/(.+)/(.+)$ https://schema.gov.it/lodview/"nome-cartella"/controlled-vocabulary/$1/$2/$3 [R=303,L]
</pre>
Le precedenti condizioni si applicano solo quando SYNTAX è html, oppure in tutti gli altri casi non gestiti dalle precedenti condizioni. Riscrivono le URL in modo diverso, reindirizzando a URL esterni basati su modelli specifici. DEVONO essere configurati sulla base del nome della cartella tematica con la quale ci si riferisce al particolare insieme di risorse semantiche nel git del w3id.

#### onto

Il file `.htaccess` da inserire nella sottocartella “italia/nome-cartella/onto” DOVREBBE essere creato a partire da [quello contenuto nella cartella del GIT “italia/onto”](https://github.com/perma-id/w3id.org/blob/master/italia/onto/.htaccess).

Esso contiene codice scritto sulla base delle Direttive Apache, e permette di gestire le richieste HTTP in base al valore dell'header Accept e di SYNTAX. A seconda del valore, le URL vengono riscritte in modo diverso o reindirizzate a URL esterni. La specifica azione di riscrittura o reindirizzamento dipende dalla combinazione di Accept e SYNTAX.

Di seguito viene data una descrizione delle direttive di esempio, alle quali DEVONO essere modificati i riferimenti degli URL di atterraggio, oltre all’eventuale modifica/integrazione delle regole al fine di meglio adattarsi al git del Contributore:

<pre>
Header set Access-Control-Allow-Origin *
</pre>
Questa riga imposta l'header Access-Control-Allow-Origin su *, consentendo a qualsiasi dominio di accedere alle risorse sul server tramite richieste Ajax o da altri domini diversi.

<pre>
Options +FollowSymLinks
</pre>
Questa riga abilita l'opzione FollowSymLinks, che permette al server di seguire i collegamenti simbolici (symlink) all'interno del file system.

<pre>
RewriteEngine on
</pre>
Questa riga attiva il motore di riscrittura delle URL di Apache (mod_rewrite), che permette di manipolare le URL delle richieste HTTP.

<pre>
SetEnvIf Accept ^.*application/rdf\+xml.* SYNTAX=rdf
SetEnvIf Accept ^.*application/rdf\+xml.* SYNTAX=owl
SetEnvIf Accept ^.*application/n-triples.* SYNTAX=n3
SetEnvIf Accept ^.*text/turtle.* SYNTAX=ttl
SetEnvIf Accept ^.*text/html.* SYNTAX=html
</pre>
Queste righe impostano una variabile di ambiente chiamata SYNTAX in base all'header Accept della richiesta HTTP. Questo viene utilizzato per determinare il tipo di sintassi richiesto nella risposta. Queste righe DEVONO essere modificate a seconda dei formati dei file presenti nelle proprie cartelle nel repository delle risorse semantiche.

<pre>
SetEnvIf Request_URI ^.*$ ROOT_URL="url-git"
</pre>
Imposta la variabile di ambiente ROOT_URL con un URL fisso. L’URL inserito DEVE essere quello del proprio repository che punta alla cartella delle ontologie (in formato `"https://raw.githubusercontent.com/..."`)

<pre>
RewriteCond %{ENV:SYNTAX} ^(rdf|ttl|owl|n3)$
RewriteRule ^([a-zA-Z-_0-9]+)(/?)$ %{ENV:ROOT_URL}$1/latest/$1.%{ENV:SYNTAX} [R=303,L]
</pre>
Definisce la regola di riscrittura dell'URL nel caso in cui il tipo file richiesto sia rdf, ttl, own o n3 (questi ultimi DEVONO essere configurati sulla base dei tipi file presenti nel repository sorgente).

<pre>
RewriteCond %{ENV:SYNTAX} ^html$
RewriteRule ^(.+)(/.+)$ https://schema.gov.it/lodview/"nome-cartella"/onto/$1$2 [R=303,L]
RewriteCond %{ENV:SYNTAX} ^html$
RewriteRule ^(.+)/$ https://schema.gov.it/lode/extract?url=https://w3id.org/italia/"nome-cartella"/onto/$1 [R=303,L]
RewriteCond %{ENV:SYNTAX} ^html$
RewriteRule ^(.+)$ https://schema.gov.it/lode/extract?url=https://w3id.org/italia/"nome-cartella"/onto/$1 [R=303,L]
</pre>
Le precedenti condizioni si applicano solo quando SYNTAX è html. Riscrivono le URL in modo diverso, reindirizzando a URL esterni basati su modelli specifici. DEVONO essere configurati sulla base del nome della cartella tematica con la quale ci si riferisce al particolare insieme di risorse semantiche nel git del w3id.

#### data

Il file `.htaccess` da inserire nella sottocartella “italia/nome-cartella/data” DOVREBBE essere creato a partire da [quello contenuto nella cartella del GIT “italia/data”](https://github.com/perma-id/w3id.org/blob/master/italia/data/.htaccess).

Esso contiene codice scritto sulla base delle Direttive Apache, e permette di configurare il server Apache per consentire l'accesso da qualsiasi dominio alle risorse del server, impostare una variabile di ambiente ROOT_URL con un valore fisso, e quindi riscrivere tutte le richieste in modo che includano ROOT_URL prima dell'URI richiesto. 

Di seguito viene data una descrizione delle direttive di esempio, alle quali DEVONO essere modificati i riferimenti degli URL di atterraggio, oltre all’eventuale modifica/integrazione delle regole al fine di meglio adattarsi al git del Contributore:

<pre>
Header set Access-Control-Allow-Origin *
</pre>
Questa riga imposta l'header Access-Control-Allow-Origin su *, consentendo a qualsiasi dominio di accedere alle risorse sul server tramite richieste Ajax o da altri domini diversi.

<pre>
Options +FollowSymLinks
</pre>
Questa riga abilita l'opzione FollowSymLinks, che permette al server di seguire i collegamenti simbolici (symlink) all'interno del file system.

<pre>
RewriteEngine on
</pre>
Questa riga attiva il motore di riscrittura delle URL di Apache (mod_rewrite), che permette di manipolare le URL delle richieste HTTP.

<pre>
SetEnvIf Request_URI ^.*$ ROOT_URL=https://schema.gov.it/lodview/"nome-cartella"/data/
</pre>
Questa riga imposta una variabile di ambiente chiamata ROOT_URL, che DEVE essere modificata sulla base del nome della cartella tematica
con la quale ci si riferisce al proprio repository di risorse semantiche su w3id.

<pre>
RewriteRule ^(.*)$ %{ENV:ROOT_URL}$1 [R=303,L]
</pre>
Questa riga è una regola di riscrittura delle URL. Ogni richiesta che arriva al server verrà riscritta in modo da includere il valore di ROOT_URL prima dell'URI richiesto. Il flag [R=303,L] indica che la risposta HTTP sarà un redirect temporaneo (codice di stato 303) e che questa è l'ultima regola da applicare.

<pre>
RewriteRule ^(.*)/$ %{ENV:ROOT_URL}$1 [R=303,L]
</pre>
Questa è una regola di riscrittura simile alla precedente, ma si applica solo alle richieste che terminano con una barra. Anche in questo caso, la risposta sarà un redirect temporaneo con codice di stato 303.

#### README.md

Per la creazione del file `README.md` si PUÒ far riferimento all’[esempio fornito da w3id.org stessa](https://github.com/perma-id/w3id.org/blob/master/dggs/README.md), oppure al [file creato sotto la cartella “/italia”](https://github.com/perma-id/w3id.org/blob/master/italia/readme.md).

In ogni caso, si DEVONO descrivere le finalità di utilizzo delle URI e indicare i nominativi dei referenti nella sezione “contatti”.
