# Contribuire al National Data Catalog

## Terminologia

Conformemente alle norme ISO/IEC Directives, Part 3 per la stesura dei documenti tecnici questo documento utilizza le parole chiave "DEVE", "DEVONO", "NON DEVE", "NON DEVONO", "DOVREBBE", "NON DOVREBBE", "PUÒ" e "OPZIONALE", la cui interpretazione è descritta di seguito.

- DEVE o DEVONO, indicano un requisito obbligatorio per rispettare le Linee Guida;
- NON DEVE o NON DEVONO, indicano un assoluto divieto delle specifiche;
- DOVREBBE o NON DOVREBBE, indicano che le implicazioni devono essere comprese e attentamente pesate prima di scegliere approcci alternativi;
- PUÒ o POSSONO o l’aggettivo OPZIONALE, indica che il lettore può scegliere di applicare o meno senza alcun tipo di implicazione o restrizione la specifica.

I termini Erogatore, Fruitore, e-service, API sono da intendersi ai sensi
del Modello di interoperabilità delle Pubbliche Amministrazioni composto
dalle Linee Guida emanate da Agid.

Il documento descrive l'interfaccia di processamento dei repository semantici
pubblicati dai vari Erogatori.

Il termine "harvesting" identifica il processo di raccolta funzionale alla pubblicazione su NDC
delle informazioni contenute nei repository semantici.
Nel quadro dell'harvesting, si adottano i seguenti termini:

* "ERRORE" indica che l'harvesting è terminato in maniera anomala;
* "WARNING" indica che l'harvesting ha notificato un messaggio di allerta
  ma il processamento non è terminato;
* "IGNORATA" indica che l'harvesting non ha processato una specifica
  risorsa (e.g. un file, una directory) ma che ciò non costituisce
  né un ERRORE né un WARNING.

## Registrazione dell'istituzione

TODO:

Come e a chi si registra l'URL del repository?
Quali altri dati descrittivi dell'istituzione sono necessari? Email?
Repository

## Contenuto del repository

Ogni repository può contenere una o più risorse semantiche
che verranno elaborate dal NDC.
Quelle supportate sono:

- Ontologie;
- Vocabolari controllati (e.g., tassonomie, code list, tesauri);
- Schemi dati in formato OAS3 (OpenAPI Specifications versione 3).
  Future versioni del catalogo possono supportare altre risorse semantiche ed altri formati.

## Layout del repository

Per essere correttamente processato, il repository deve rispettare una serie di regole
che rendono il processamento semplice ed efficiente.

Il repository DEVE contenere i seguenti file:

- publiccode.yaml: contenente tutte le informazioni richieste dal Catalogo del Riuso.

Un repository è un oggetto pubblico indicizzato dal Catalogo del Riuso,
e DEVE contenere un file `publiccode.yml` conforme alle relative Linee Guida
col riferimento al codice IPA dell'ente che gestore.
Queste informazioni verranno utilizzate anche per la continuità operativa del NDC.

```yaml
...
maintenance:
  contacts:
email: info@teamdigitale.governo.it
name: Dipartimento per la Trasformazione Digitale
it:
  riuso:
    codiceIPA: pcm
```

Tutte le risorse fornite DEVONO risiedere nella directory `asset/`.
Le risorse al di fuori di `asset/` non saranno elaborate.

Ogni tipo di asset (ontologie, vocabolari controllati, schemi)
DEVE risiedere in una directory specifica con un nome predefinito.

I nomi di file e directory DEVONO corrispondere al pattern :code:`[A-Za-z0-9_.-]{, 64}`,
non possono quindi contenere spazi.
Le directory associate ai dataset DOVREBBERO essere in minuscolo.

I contenuti degli asset DEVONO essere codificati in UTF-8.

Ogni risorsa DEVE risiedere sotto una sua directory specifica dipendente dalla sua tipologia:

* Ontologie: in :code:`assets/ontologies/`;
* Vocabolari controllati: in :code:`assets/controlled-vocabularies/`;
* Schemi: in assets/schemas/.

Ad esempio:
il percorso dell'ontologia MyOntology sarà assets/ontologies/MyOntology/
il percorso del Vocabolario my-vocabulary sarà assets/controlled-vocabularies/my-vocabulary/

## Documentazione

Le directory degli asset POSSONO contenere file di documentazione in formato Markdown.
L'estensione del file DEVE essere .md (ad esempio README.md).
Questi file vengono ignorati durante il processamento da parte di NDC.

## Esempi

A titolo di esempio, si consideri un repository che abbia la struttura delle directory come quella di seguito.

```bash
┌─ publiccode.yaml
┌─ assets/ontologies/
│  ├─ Onto1/
│  │  ├─ onto1.ttl
│  │  └─ onto1.rdf
│  ├─ Sottoargomento/
│  │  ├─ Onto2/
│  │  │  └─ onto2.xml
│  │  ├─ Onto3/
│  │  │  └─ onto3.ttl
│  ├─ Onto4/
│  │  ├─ Other/
│  │  │  └─ temp.md
│  │  └─ onto4.ttl
│  └─ notes.md
├─ assets/controlled-vocabularies/
│  └─ ...
└─ README.md
```

Il repository non contiene schemi, quindi NDC non aggiungerà schemi al catalogo durante l'harvesting.
Questo non rappresenta un problema e non è considerato un errore;
dei file informativi (e.g. README.md, notes.md) sono presenti sia nella radice che 
nelle sottodirectory: questi file vengono ignorati durante l'harversting.

Per quanto riguarda la directory Onto1:

* essa non contiene sotto-directory né altre directory al suo interno
  ed è quindi una cartella foglia.
  Quindi viene processata come potenzialmente contenente un'ontologia;
* contiene un file RDF/Turtle che verrà processato;
* contiene un altro file RDF, plausibilmente una serializzazione diversa degli stessi contenuti del file .ttl in RDF/XML.
  Poiché NDC processa solo i file di tipo text/turtle con estensione .ttl, questo file viene ignorato.

L'Erogatore ha organizzato logicamente le directory Onto2 e Onto3
come subdirectory di Sottoargomento.
Questo non rappresenta un problema e le directory vengono harvestate.
Essendo, a loro volta, directory foglia sono considerate come potenziali contenitori di ontologie.

La directory Onto2 non contiene file .ttl: questo viene segnalato solamente come WARNING.

La directory Onto4 ha una sottodirectory, quindi non è considerata come contenitore di ontologia,
bensì come directory intermedia nel cammino per altre directory foglia:
il file onto4.tll è ignorato e non processato.

## Versionamento

Le directory degli asset POSSONO essere avere sub-directory 
per supportare il versionamento. 
Il nome delle sub-directory DEVE corrispondere al pattern:

(latest|v?[0-9]+(\.[0-9]+){0,2}).

Una directory contenente  asset NON DEVE contenere contemporaneamente sub-directory versionate con e senza il prefisso v.

Sei esempi di path validi per le sub-directory:

```
assets/ontologies/MyOntology/202101/
assets/ontologies/MyOntology/1.3/
assets/ontologies/MyOntology/4.5.6/
assets/ontologies/MyOntology/v1.3/
assets/ontologies/MyOntology/v4.5.6/
assets/schemas/Person/latest/
```

Sei esempi di path non validi

```
assets/ontologies/MyOntology/v.5
assets/ontologies/MyOntology/4.3.
assets/ontologies/MyOntology/v1..5
assets/ontologies/MyOntology/versione 2.9
v1.5-beta
```

Ordinamento delle versioni

Il Catalogo elabora solo:

- la directory latest se presente;
- la directory con l'ultima versione, secondo l'ordinamento indicato dal semantic versioning.

Nota: Il versionamento si applica solamente alle Ontologie.

All'interno di un repository è possibile mantenere versioni precedenti delle ontologie per tenere traccia di uno storico, al di là del supporto che fornisce lo strumento git.
L'harvesting delle ontologie considera che le directory che contengono ontologie possano essere versionate, non i singoli file. Questo vale anche per le sotto-directory.
In un qualsiasi punto della gerarchia delle directory che occorrono all'interno della cartella Ontologie, qualora vi siano più directory i cui nomi rappresentino delle versioni, la logica di harvesting ignorerà tutte le directory precedenti all'ultima, considerandole obsolete.

Come si rappresentano le versioni

I nomi delle directory, per essere considerate tabelle di versione, devono avere un nome che segue il seguente pattern:
v?[0-9]+(\.[0-9]+){0,2}
un carattere iniziale v, opzionale.
un numero di versione
opzionalmente una serie di coppie punto (.) seguito da un altro numero, per indicare sotto versioni.
Come unica eccezione al pattern appena descritto, è supportato il nome latest, che rappresenta la versione più recente confrontata rispetto a qualsiasi altra versione numerata.
A titolo di esempio, sono validi nomi di directory per le versioni:

```
v1, v2 ma anche semplicemente 1 e 2
v1.3, v4.5.6 e anche 1.3, 4.5.6
```

Non sono validi

```
v.5
4.3.
v1..5
versione 2.9
v1.5-beta
```

## Ordinamento delle versioni

latest è sempre più recente di qualsiasi altra versione
Tra due versioni espresse come forme numeriche (con punti), si segue l'ordinamento comunemente condiviso per cui i numeri a sinistra sono i più significativi
Qualora due versioni abbiano lunghezza diversa ma una sia prefisso dell'altra, la più lunga viene considerata più recente; ad esempio v4.5 è considerata obsoleta in presenza di v4.5.2.
Dove possono trovarsi le directory versionate
La directory versionate possono trovarsi in ogni punto dell'alberatura della directory delle ontologie, discendendo verso le foglie della struttura gerarchica.

Sono esempi validi:

```bash
┌─ Ontologie/
│  ├─ Onto1/
│  │  ├─ latest/
│  │  │  └─ onto1.ttl
│  │  ├─ v0.5/
│  │  │  └─ onto1.ttl
│  │  ├─ v0.6/
│  │  │  └─ onto1.ttl
│  ├─ Onto2/
│  │  ├─ 0.5/
│  │  │  └─ onto2.ttl
│  │  └─ 0.6/
│  │     └─ onto2.ttl
│  └─ ...
└─ ...
```

Nel caso della struttura precedente, ogni ontologia ha diverse versioni al proprio interno.
È altresì valido un approccio in cui si strutturano in versioni insiemi di directory di ontologie, come segue:

```bash
┌─ Ontologie/
│  ├─ latest/
│  │  ├─ Onto1/
│  │  │  └─ onto1.ttl
│  │  ├─ Onto2/
│  │  │  └─ onto2.ttl
│  ├─ v0.8/
│  │  ├─ Onto1/
│  │  │  └─ onto1.ttl
│  │  ├─ Onto2/
│  │  │  └─ onto2.ttl
│  │  └─ Onto3/
│  │     └─ onto3.ttl
│  └─ ...
└─ ...
```

Si noti, per esempio, che questo permette di rimuovere dal catalogo anche versioni precedenti di ontologie che, nella versione più recente, non si vogliono più pubblicare. Nell'esempio precedente, infatti, il file onto3.ttl non sarebbe processato, poiché durante la navigazione delle directory, la directory v0.8 è saltata perché considerata come resa obsoleta dalla presenza della sorella latest.
Qualora fosse necessario versionare gruppi di ontologie che variano più frequentemente nel tempo, mentre mantenerne stabili altre, è possibile raggruppare in versioni solo quelle che variano. Durante la navigazione, infatti, sono ignorate le directory che contengono versioni obsolete di contenuti aggiornati, mentre le directory i cui nomi non rappresentano versioni sono processari normalmente.
Il seguente esempio illustra questa possibilità (i contenuti delle directory foglia sono omessi per brevità):

```bash
┌─ Ontologie/
│  ├─ latest/
│  │  ├─ Onto1/
│  │  └─ Onto2/
│  ├─ v0.8/
│  │  ├─ Onto1/
│  │  └─ Onto2/
│  ├─ Onto3/
│  ├─ Onto4/
│  └─ ...
└─ ...
```

In questo esempio le ontologie contenute in Onto3 e Onto4 sono stabili, per cui non vale la pena di replicarle in diverse directory. Diversamente le ontologie in Onto1 e Onto2 sono aggiornate e, plausibilmente, vengono aggiornate di pari passo perché hanno una qualche correlazione; può valere la pena evolvere la loro versione parallelamente.

Nessuna rappresentazione RDF alternativa
Le directory degli asset NON DEVONO contenere risorse RDF in altre serializzazioni (ad es. RDF / XML, JSON-LD, ..). Queste non saranno elaborate.

Questi file POSSONO essere inseriti nello stesso repository al di fuori della directory asset/; In questo caso, essi DOVREBBERO essere generati automaticamente dai file originali in asset/.

## Ontologie

Le ontologie pubblicate DEVONO essere conformi alle relative Linee guida nazionali.

Le ontologie DEVONO essere pubblicate solo in formato RDF/Turtle (media-type text/turtle) e l'estensione del file DEVE essere .ttl.

Le ontologie DEVONO utilizzare delle directory versionate come descritto sopra.

Esempio di alberatura contenente i file che definiscono un'ontologia. In questo caso viene processata solo la directory latest/. Nell'esempio, l'alberatura contiene una serie di file di documentazione opzionali che non vengono processati.

```bash
assets/
  ontologies/
    MyOntology/
      CHANGELOG.md
      README.md
      v1.2/
        MyOntology.ttl
      v1.1/
        MyOntology.ttl
      latest/
        MyOntology.ttl
        LATEST.md
```

## Vocabolari controllati

I vocabolari controllati pubblicati DEVONO essere conformi agli associati Linee guida nazionali.

I vocabolari controllati DEVONO essere pubblicati solo in formato RDF/Turtle (media-type text/turtle) e l'estensione del file DEVE essere .ttl.

Le directory del vocabolario controllato DOVREBBERO contenere una proiezioni in formato CSV del vocabolario insieme ai metadati necessari per mappare i campi del CSV alle risorse presenti nell'RDF: Questa proiezione in formato CSV sarà esposta dalla NDC tramite API REST. L'estensione del file DEVE essere .csv.

I metadati di cui sopra DEVONO essere espressi tramite un @context JSON-LD 1.1.

Di seguito l'esempio di un'alberatura contenente un vocabolario controllato e la sua proiezione in formato CSV.

assets/
  controlled-vocabulary/
    my-codelist/
      CHANGELOG.md
      README.md
      my-codelist.ttl
      my-codelist.csv

## Schemi

Gli schemi pubblicati devono essere conformi agli associati Linee guida nazionali.

Gli schemi per le API dell'OAS3 devono essere pubblicati in formato OpenAPI3, incorporato nella sezione #/components/schema del file OAS.
L'estensione del file DEVE essere .oas3.yaml.

In futuro potranno essere supportati altri tipi di schemi.

Il file YAML DOVREBBE contenere i riferimenti semantici attraverso:

- il campo custom `x-jsonld-context` contenente un `@context` JSON-LD conforem alle indicazioni contenute in JSON-LD 1.1;
- il campo custom `x-jsonld-type` contenente il riferimento ad un `rdf:type`.

Un esempio di file OAS3 metadatato con il campo `x-jsonld-context`:

```yaml
openapi: 3.0.1
...
components:
  schemas:
    Person:
      type: object
      x-jsonld-context:
        "@vocab": "https://w3id.org/italia/onto/CPV/"
        nome_proprio: givenName
        cognome: familyName
      properties:
        nome_proprio: {type: string, ..}
        cognome: {type: string, ..}
      ...
```

I metadati associati DEVONO essere pubblicati solo in formato RDF/Turtle (media type `text/turtle`) e l'estensione del file DEVE essere `.ttl`.
Questo file DOVREBBE essere generato automaticamente dal documento OAS3.

Gli schemi forniti POSSONO essere verificati sintatticamente utilizzando l'[OpenAPI Checker](https://github.com/italia/api-oas-checker).

Di seguito l'esempio di un'alberatura contenente uno schema

```bash
assets/
  schemas/
    Person/
      CHANGELOG.md
      README.md
      person.oas3.yaml
      person.index.ttl
```

## Controlli automatici

Il repository DOVREBBE utilizzare strumenti di continuous integratio come github-actions o gitlab-ci per verificare la consistenza dei contenuti.
