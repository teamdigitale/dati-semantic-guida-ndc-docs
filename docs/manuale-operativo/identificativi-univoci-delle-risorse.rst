Identificativi univoci delle risorse 
=====================================

Nel contesto del Web semantico, c’è necessità di definire i cosiddetti
"URI stabili/permanenti", ovvero:

- che rimangano stabili per un tempo indeterminato, in quanto fanno
  riferimento a entità che devono essere permanenti e univoche;

- che permettano di essere risolti su una pagina web o simili per avere
  informazioni;

- nella forma
  ``https://{{dominio}}/{{tipo_risorsa}}/{{concetto}}/{{codice_riferimento}}``,
  dove:

   * il \ **dominio**, il cui valore dipende dalla scelta effettuata
     dai Contributori (rif. `Scelta degli identificativi univoci nel web <../premesse/scelta-degli-identificativi-univoci-nel-web.html>`__);

   * il **tipo di risorsa** può essere, ad esempio, uno dei seguenti
     valori:

      + onto: per rappresentare tutto il mondo delle ontologie

      + controlled-vocabulary: per rappresentare tutto il mondo dei
        vocabolari controllati

      + data: per specificare gli URI dei dati collegati (linked data)
        che sono creati come istanze dei modelli ontologici

   * il \ **concetto** è lo specifico concetto che si istanzia nei dati
     o nome dell'ontologia;

   * il **codice di riferimento** è il codice univoco per identificare
     univocamente la "cosa" descritta.

Per ulteriori indicazioni in merito, fare riferimento alle `Linee Guida
Open Data di
AgID <https://www.agid.gov.it/sites/default/files/repository_files/lg-open-data_v.1.0_1.pdf>`__.

Ciò detto, i Contributori possono seguire integralmente le indicazioni
nella presente sezione, sia in termini di configurazione dei file di
redirect che di definizione di URI, nel caso in cui vogliano pubblicare
risorse semantiche in un proprio repository e **non abbiano già
implementato una propria soluzione per le URI stabili**. Al contrario,
se i Contributori hanno già implementato una propria soluzione per le
URI stabili, potranno continuare ad utilizzarla anche nel contesto del
Catalogo, senza dover seguire le indicazioni nella presente sezione.

Introduzione al redirect con w3id.org
-------------------------------------

`w3id.org <https://w3id.org/>`__ è una soluzione del W3C Permanent
Identifier Community Group che permette l’aggiunta o modifica di
identificativi permanenti a partire dai quali reindirizzare verso URL
specifici; il processo si basa sull’aggiunta di una o più cartelle nel
`repository git del
w3id <https://github.com/perma-id/w3id.org/blob/master/italia/readme.md>`__
le quali contengono i file '.htaccess' e file 'README.md',
eventualmente organizzati in sottocartelle.

Nel caso del Catalogo si può richiedere la
registrazione di un proprio dominio su w3id creando una cartella
dedicata oppure facendo riferimento alla `cartella Italia del GIT del w3id <https://github.com/perma-id/w3id.org/tree/master/italia>`__, nella
quale possono essere aggiunte le sottocartelle, ciascuna per una
particolare area tematica, contenenti i file di reindirizzamento,
eventualmente organizzati in ulteriori sottocartelle, ed il file
'README.md'; successivamente, le stesse saranno gestite autonomamente e
con interfacciamento diretto verso w3id.org dai referenti indicati nei
file 'README.md'. La cartella e le relative sottocartelle, i file
'.htaccess' e i file 'README.md' sono creati sul `repository git del
w3id <https://github.com/perma-id/w3id.org/tree/master/italia>`__ dal
Contributore.

Una nota importante è che l'efficacia delle regole di redirect descritte
nei seguenti paragrafi è subordinata all'applicazione delle indicazioni
offerte dalla presente guida per la creazione ed organizzazione del
repository contenente le risorse semantiche, con particolare riferimento
all'uguaglianza che deve persistere tra il nome di ciascuna cartella e
il nome dei relativi file, a meno dell'estensione, e il nome con il
quale viene referenziata la risorsa semantica (ontologia) all'interno
del proprio URI.

Processo di pubblicazione degli htaccess
----------------------------------------

Fork del repository git del w3id
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Il primo passo per la registrazione dei vari redirect è il fork in
locale del `repository del w3id <https://github.com/perma-id/w3id.org>`__.

Gli identificativi permanenti (URI) verranno definiti sulla base del
percorso nel quale saranno inseriti i vari file 'htaccess'. Nel caso si
vogliano registrare URI sotto la cartella Italia, allora il percorso
della cartella 'root' per 'nome-cartella' dovrà essere
'italia/<nome-cartella>/' dunque il namespace degli URI
definiti nella stessa sarà 'w3id.org/italia/<nome-cartella>/'.

Aggiunta della cartella
~~~~~~~~~~~~~~~~~~~~~~~

Nel repository in locale creato a partire dalla fork occorrerà creare la
cartella sotto 'italia' oppure direttamente sotto la cartella 'root', e
che conterrà l’alberatura di sottocartelle e dei relativi file
'.htaccess', oltre al file 'README.md', la cui creazione e
configurazione è a carico del Contributore. A tal proposito, in 
coda alla sezione sono disponibili una guida alla creazione dei file 
e alcuni esempi di possibili strumenti da utilizzare per i test del redirect.

Di seguito è fornito un esempio di alberatura della cartella sotto
'/italia':

::

   italia
   |--nome-cartella
   |  |--controlled-vocabulary
   |  |  |-.htaccess
   |  |--data
   |  |  |-.htaccess
   |  |--onto
   |  |  |-.htaccess
   |  |README.md

In tal modo, verranno definiti i seguenti URI stabili:

-  w3id.org/italia/<nome-cartella>/controlled-vocabulary

-  w3id.org/italia/<nome-cartella>/data

-  w3id.org/italia/<nome-cartella>/onto

Il '<nome-cartella>' è molto importante dato che dovrà essere inserito
in specifici parametri descritti di seguito, e sarà sempre utilizzato
per riferirsi all'insieme delle risorse semantiche del Contributore
nell'ambito della configurazione dei file di redirect.

Le regole di redirect associate a ciascun URI sono definite nei relativi
file '.htaccess'. Il file 'README.md' contiene i nominativi dei
referenti unitamente ai loro riferimenti e-mail e di github. Questi
riferimenti curano la gestione della cartella e dei relativi file a
seguito dell’approvazione di 'Italia'. È opportuno prendere come esempio
il file 'README.md' sotto la cartella 'italia'.

Creazione della pull request
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Una volta modificato il repository GIT in locale, si crea una pull
request; nel caso in cui si stiano registrando URI sotto Italia, occorre
indicare come reviewer della pull request i contatti presenti nel file
`readme sotto
Italia <https://github.com/perma-id/w3id.org/blob/master/italia/readme.md>`__,
che procederanno all’analisi e conseguente validazione della stessa.

Il merge sul branch master verrà effettuato in ogni caso direttamente da
w3id.org e determinerà la pubblicazione definitiva dei nuovi URI e
relative regole di redirect.

Contenuto dei file htaccess e readme
------------------------------------

Di seguito è data una descrizione del file '.htaccess' per ciascuna
tipologia di risorsa, da cui il Contributore può prendere spunto per
creare i propri file di redirect. Gli esempi sono calati nella casistica
in cui il Contributore voglia iscrivere le proprie URI sotto
w3id.org/italia/dominio_specifico, voglia fruire delle soluzioni di *URI
dereferentiation* implementate in Schema, e abbia rispettato le
indicazioni sulla creazione del repository sorgente per le proprie
risorse semantiche descritte in `Istruzioni su come predisporre il repository <../manuale-operativo/istruzioni-su-come-predisporre-il-repository-in-cui-pubblicare-le-risorse-semantiche.html>`__.
In casi diversi rispetto al precedente, il Contributore dovrà adeguare
opportunamente le regole di redirect descritte di seguito.

controlled-vocabulary
~~~~~~~~~~~~~~~~~~~~~

È buona norma creare il file '.htaccess' da inserire nella
sottocartella
'…/nome-cartella/controlled-vocabulary' prendendo
come esempio quello contenuto nella `cartella del GIT
'italia/controlled-vocabulary' <https://github.com/perma-id/w3id.org/blob/master/italia/controlled-vocabulary/.htaccess>`__.

Esso contiene codice scritto sulla base delle Direttive Apache, e
permette di gestire le richieste HTTP in base al valore dell'header
Accept e di SYNTAX. A seconda del valore, gli URL vengono riscritti in
modo diverso o reindirizzati a URL esterni. La specifica azione di
riscrittura o reindirizzamento dipende dalla combinazione di Accept e
SYNTAX.

Di seguito viene data una descrizione delle direttive di esempio, alle
quali sono modificati i riferimenti degli URL di atterraggio, oltre
all’eventuale modifica/integrazione delle regole al fine di meglio
adattarsi al git del Contributore:

::

   Header set Access-Control-Allow-Origin *

Questa riga imposta l'header Access-Control-Allow-Origin su \*,
consentendo a qualsiasi dominio di accedere alle risorse sul server
tramite richieste Ajax o da altri domini diversi.

::

   Options +FollowSymLinks

Questa riga abilita l'opzione FollowSymLinks, che permette al server di
seguire i collegamenti simbolici (symlink) all'interno del file system.

::

   RewriteEngine on

Questa riga attiva il motore di riscrittura degli URL di Apache
(mod_rewrite), che permette di manipolare gli URL delle richieste HTTP.

::

   SetEnvIf Accept ^.*text/turtle.* SYNTAX=ttl

   SetEnvIf Accept ^.*application/json.* SYNTAX=json

   SetEnvIf Accept ^.*application/csv.* SYNTAX=csv

   SetEnvIf Accept ^.*text/csv.* SYNTAX=csv

   SetEnvIf Accept ^.*text/html.* SYNTAX=html

Queste righe impostano una variabile di ambiente chiamata SYNTAX in base
all'header Accept della richiesta HTTP. Questo viene utilizzato per
determinare il tipo di sintassi richiesto nella risposta. Queste righe
sono modificate a seconda dei formati dei file presenti nelle proprie
cartelle github.

::

   SetEnvIf Request_URI ^.*$ ROOT_URL=<url-git>

Imposta la variabile di ambiente ROOT_URL con un URL fisso. L’URL
inserito è quello del proprio Github che punta alla cartella dei
vocabolari controllati (in formato https://raw.githubusercontent.com/...).

::

   RewriteCond %{ENV:SYNTAX} ^(ttl|json|csv)$

   RewriteRule ^([a-zA-Z-_0-9]+)(/?)$ %{ENV:ROOT_URL}$1/latest/$1.%{ENV:SYNTAX} [R=303,L]

Definisce la regola di riscrittura dell'URL nel caso in cui il tipo file
richiesto sia ttl, json o csv (questi ultimi sono configurati sulla base
dei tipi file presenti nel repository sorgente).

::

   RewriteCond %{ENV:SYNTAX} ^html$

   RewriteRule ^(.+)$ https://schema.gov.it/lodview/<nome-cartella>/controlled-vocabulary/$1 [R=303,L]

   RewriteRule ^(.+)/(.+)/(.+)$ https://schema.gov.it/lodview/<nome-cartella>/controlled-vocabulary/$1/$2/$3 [R=303,L]

Le precedenti condizioni si applicano solo quando SYNTAX è html, oppure
in tutti gli altri casi non gestiti dalle precedenti condizioni.
Riscrivono gli URL in modo diverso, reindirizzando a URL esterni basati
su modelli specifici. Al posto di <nome-cartella> occorre inserire il
nome della cartella tematica aggiunta sotto '/italia' nel git del w3id
con la quale ci si riferisce al particolare insieme di risorse
semantiche.

onto
~~~~

È buona norma creare il file '.htaccess' da inserire nella
sottocartella 'nome-cartella/onto' a partire da quello
contenuto nella `cartella del GIT
'italia/onto' <https://github.com/perma-id/w3id.org/blob/master/italia/onto/.htaccess>`__.

Esso contiene codice scritto sulla base delle Direttive Apache, e
permette di gestire le richieste HTTP in base al valore dell'header
Accept e di SYNTAX. A seconda del valore, le URL vengono riscritti in
modo diverso o reindirizzati a URL esterni. La specifica azione di
riscrittura o reindirizzamento dipende dalla combinazione di Accept e
SYNTAX.

Di seguito viene data una descrizione delle direttive di esempio, alle
quali sono modificati i riferimenti degli URL di atterraggio, oltre
all’eventuale modifica/integrazione delle regole al fine di meglio
adattarsi al git del Contributore:

::

   Header set Access-Control-Allow-Origin *

Questa riga imposta l'header Access-Control-Allow-Origin su \*,
consentendo a qualsiasi dominio di accedere alle risorse sul server
tramite richieste Ajax o da altri domini diversi.

::

   Options +FollowSymLinks

Questa riga abilita l'opzione FollowSymLinks, che permette al server di
seguire i collegamenti simbolici (symlink) all'interno del file system.

::

   RewriteEngine on

Questa riga attiva il motore di riscrittura degli URL di Apache
(mod_rewrite), che permette di manipolare gli URL delle richieste HTTP.

::

   SetEnvIf Accept ^.*application/rdf\+xml.* SYNTAX=rdf

   SetEnvIf Accept ^.*application/rdf\+xml.* SYNTAX=owl

   SetEnvIf Accept ^.*application/n-triples.* SYNTAX=n3

   SetEnvIf Accept ^.*text/turtle.* SYNTAX=ttl

   SetEnvIf Accept ^.*text/html.* SYNTAX=html

Queste righe impostano una variabile di ambiente chiamata SYNTAX in base
all'header Accept della richiesta HTTP. Questo viene utilizzato per
determinare il tipo di sintassi richiesto nella risposta. Queste righe
sono modificate a seconda dei formati dei file presenti nelle proprie
cartelle nel repository delle risorse semantiche.

::

   SetEnvIf Request_URI ^.*$ ROOT_URL=<url-git>

Imposta la variabile di ambiente ROOT_URL con un URL fisso. L’URL
inserito è quello del proprio repository che punta alla cartella delle
ontologie (in formato https://raw.githubusercontent.com/...).

::

   RewriteCond %{ENV:SYNTAX} ^(rdf|ttl|owl|n3)$

   RewriteRule ^([a-zA-Z-_0-9]+)(/?)$ %{ENV:ROOT_URL}$1/latest/$1.%{ENV:SYNTAX} [R=303,L]

Definisce la regola di riscrittura dell'URL nel caso in cui il tipo file
richiesto sia rdf, ttl, own o n3 (questi ultimi sono configurati sulla
base dei tipi file presenti nel repository sorgente).

::

   RewriteCond %{ENV:SYNTAX} ^html$

   RewriteRule ^(.+)(/.+)$ https://schema.gov.it/lodview/<nome-cartella>/onto/$1$2 [R=303,L]

   RewriteCond %{ENV:SYNTAX} ^html$

   RewriteRule ^(.+)/$ https://schema.gov.it/lode/extract?url=https://w3id.org/italia/<nome-cartella>/onto/$1 [R=303,L]

   RewriteCond %{ENV:SYNTAX} ^html$

   RewriteRule ^(.+)$ https://schema.gov.it/lode/extract?url=https://w3id.org/italia/<nome-cartella>/onto/$1 [R=303,L]

Le precedenti condizioni si applicano solo quando SYNTAX è html.
Riscrivono gli URL in modo diverso, reindirizzando a URL esterni basati
su modelli specifici. Al posto di <nome-cartella> occorre inserire il
nome della cartella tematica aggiunta sotto '/italia' nel git del w3id
con la quale ci si riferisce al particolare insieme di risorse
semantiche.

data
~~~~

È bene che il file '.htaccess' da inserire nella sottocartella
'…/nome-cartella/data' sia essere creato a partire da quello
contenuto nella `cartella del GIT
'italia/data' <https://github.com/perma-id/w3id.org/blob/master/italia/data/.htaccess>`__.

Esso contiene codice scritto sulla base delle Direttive Apache, e
permette di configurare il server Apache per consentire l'accesso da
qualsiasi dominio alle risorse del server, impostare una variabile di
ambiente ROOT_URL con un valore fisso, e quindi riscrivere tutte le
richieste in modo che includano ROOT_URL prima dell'URI richiesto.

Di seguito viene data una descrizione delle direttive di esempio, alle
quali sono modificati i riferimenti degli URL di atterraggio, oltre
all’eventuale modifica/integrazione delle regole al fine di meglio
adattarsi al git del Contributore:

::

   Header set Access-Control-Allow-Origin *

Questa riga imposta l'header Access-Control-Allow-Origin su \*,
consentendo a qualsiasi dominio di accedere alle risorse sul server
tramite richieste Ajax o da altri domini diversi.

::

   Options +FollowSymLinks

Questa riga abilita l'opzione FollowSymLinks, che permette al server di
seguire i collegamenti simbolici (symlink) all'interno del file system.

::

   RewriteEngine on

Questa riga attiva il motore di riscrittura degli URL di Apache
(mod_rewrite), che permette di manipolare gli URL delle richieste HTTP.

::

   SetEnvIf Request_URI ^.*$ ROOT_URL=https://schema.gov.it/lodview/<nome-cartella>/data/

Questa riga imposta una variabile di ambiente chiamata ROOT_URL, dove al
posto di <nome-cartella> occorre inserire il nome della cartella
tematica aggiunta sotto '/italia' nel git del w3id con la quale ci si
riferisce al particolare insieme di risorse semantiche.

::

   RewriteRule ^(.*)$ %{ENV:ROOT_URL}$1 [R=303,L]

Questa riga è una regola di riscrittura degli URL. Ogni richiesta che
arriva al server verrà riscritta in modo da includere il valore di
ROOT_URL prima dell'URI richiesto. Il flag [R=303,L] indica che la
risposta HTTP sarà un redirect temporaneo (codice di stato 303) e che
questa è l'ultima regola da applicare.

::

   RewriteRule ^(.*)/$ %{ENV:ROOT_URL}$1 [R=303,L]

Questa è una regola di riscrittura simile alla precedente, ma si applica
solo alle richieste che terminano con una barra. Anche in questo caso,
la risposta sarà un redirect temporaneo con codice di stato 303.

README.md
~~~~~~~~~

Per la creazione del file 'README.md' è possibile far riferimento

-  `all’esempio fornito da w3id.org
   stessa <https://github.com/perma-id/w3id.org/blob/master/dggs/README.md>`__;

-  `al file creato sotto la cartella
   '/italia' <https://github.com/perma-id/w3id.org/blob/master/italia/readme.md>`__.

In ogni caso, nella sezione'contatti' del file readme occorre
descrivere le finalità di utilizzo degli URI e indicare i nominativi dei
referenti specificando il loro contatto github e possibilmente
un’e-mail.

Esempi di strumenti a supporto dei test
---------------------------------------

Il Contributore è responsabile della scrittura ed eventuale correzione
dei file htaccess che vengono pubblicati sul w3id; pertanto, è tenuto a
verificarne la correttezza.

A titolo di esempio, un possibile approccio per testare gli htaccess
prima della pubblicazione sul w3id potrebbe basarsi sull'installazione
di un server Apache, in un container o macchina virtuale, e la
configurazione dei file htaccess all'interno di esso. Questo
consentirebbe di eseguire test approfonditi sui redirect a partire dal
server di test.

Per i test successivi alla pubblicazione su w3id dei file htaccess e
dell’harvesting sul Catalogo, un'opzione può essere l'utilizzo di cURL
per verificare la correttezza delle regole di redirect. In particolare,
in ciascuno dei file htaccess sono definite una o più regole di redirect
basate sul contenuto (es. html, rdf, turtle, ecc.). 
Per testare tutte le regole, occorre innanzitutto individuare URI utili a
stressare le regole di redirect contenute in tutti i file htaccess
(onto, controlled-vocabulary e data). Successivamente, per ciascuna
tipologia di risorsa occorre testare, con l’URI individuato, tutti i
possibili contenuti gestiti dal relativo file htaccess, e verificare che
il redirect sia quello atteso. In caso contrario, il Contributore dovrà
aprire una pull request sul git del w3id al fine di correggere il file
htaccess.

La generica riga di comando in input da inserire nel prompt dei comandi
è la seguente:

::

   curl [URI] --header “Accept: [Content type]”

Di seguito viene fornito un esempio di utilizzo di cURL per verificare
la correttezza dei redirect nel caso di una ontologia.

.. figure:: ../../media/image13.png
   :alt: Figura 13 Prompt dei comandi- cURL per verifica redirect
   :width: 6.5in
   :height: 1.22431in

   Figura 13 Prompt dei comandi- cURL per verifica redirect

Nel caso d’esempio, l’URI fornito è il seguente:
https://w3id.org/italia/work-accident/onto/core/, mentre il contenuto
richiesto è 'text/html', ovvero uno di quelli gestiti dal relativo `file
htaccess <https://github.com/perma-id/w3id.org/blob/master/italia/work-accident/onto/.htaccess>`__
per le ontologie. Il risultato della cURL mostra come stato http il
valore '303 See Other', che indica che l’indirizzamento avviene
con successo, e come indirizzo di atterraggio quello costruito
dall’apposita regola di redirect nel htaccess, come atteso.