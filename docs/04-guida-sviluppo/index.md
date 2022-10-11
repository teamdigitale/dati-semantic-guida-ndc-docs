# Contribuire al National Data Catalog

Il documento descrive l’interfaccia di processamento dei repository semantici
pubblicati dai vari Erogatori.

L'architettura del NDC è definita in [Architettura](architettura)

## Terminologia

Questa sezione utilizza le definizioni e gli acronimi
indicati nel Capitolo 2, oltre ai termini definiti di seguito.

Il termine "harvesting" identifica il processo di raccolta funzionale alla pubblicazione su NDC
delle informazioni contenute nei repository semantici.
Nel quadro dell’harvesting, si adottano i seguenti termini:

* "ERRORE" indica che l’harvesting è terminato in maniera anomala;
* "WARNING" indica che l’harvesting ha notificato un messaggio di allerta
  ma il processamento non è terminato;
* "IGNORATA" indica che l’harvesting non ha processato una specifica
  risorsa (e.g. un file, una directory) ma che ciò non costituisce
  né un ERRORE né un WARNING.

## Registrazione dell’istituzione

TODO:

Come e a chi si registra l’URL del repository?
Quali altri dati descrittivi dell’istituzione sono necessari? Email?
Repository

## Contenuto del repository

Ogni repository può contenere una o più risorse semantiche
che verranno elaborate dal NDC.
Quelle supportate sono:

* Ontologie;
* Vocabolari controllati (e.g., tassonomie, code list, tesauri);
* Schemi dati in formato [OAS3] (OpenAPI Specifications versione 3).
  Future versioni del catalogo possono supportare altre risorse semantiche ed altri formati.

## Formati supportati

I file DEVONO essere codificati in UTF-8.

Tutti i file RDF DEVONO essere pubblicati in formato Turtle (media type `text/turtle`).
L’estensione del file DEVE essere `.ttl`.
Ulteriori serializzazioni (e.g. RDF/XML, JSON-LD, ..):

* non verranno processate da NDC;
* NON DOVREBBERO essere pubblicate, poiché verranno generate automaticamente
  dal NDC a partire dai file Turtle;
* se presenti, DOVREBBERO essere generate automaticamente a partire dalla serializzazione in formato Turtle.

I file OAS3, JSON e JSON-LD DEVONO essere pubblicati in formato YAML,
usando l’estensione `.yaml` o `.yamlld` a seconda del formato.

## Controlli automatici

Il repository DOVREBBE utilizzare strumenti di continuous integration
come github-actions o gitlab-ci per verificare la consistenza dei contenuti
e la sintassi dei file.

Il modello di repository per gli asset semantici <https://github.com/teamdigitale/dati-semantic-cookiecutter>
contiene degli esempi di controlli eseguibili sia in locale che nelle pipeline
di continuous integration che verificano, tra l'altro:

* la validità sintattica degli asset semantici;
* la consistenza dello stile adottato per la pubblicazione.

[PUBLICCODE_YML]: https://docs.italia.it/italia/developers-italia/publiccodeyml/
[OAS3]: https://spec.openapis.org/oas/v3.0.3
[IPA]: https://indicepa.gov.it


## Layout del repository

Per essere correttamente processato, il repository deve rispettare una serie di regole
che rendono il processamento semplice ed efficiente.

Un repository è un oggetto pubblico indicizzato dal Catalogo del Riuso,
e DEVE contenere il file `publiccode.yml` conforme alle relative Linee Guida [PUBLICCODE_YML]
col riferimento al Codice [IPA] dell’Erogatore.
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

Ogni risorsa DEVE risiedere sotto una sua directory specifica dipendente dalla sua tipologia:

* Ontologie: in `assets/ontologies/`;
* Vocabolari controllati: in `assets/controlled-vocabularies/`;
* Schemi: in `assets/schemas/`.

I nomi di file e directory DEVONO rispettare il pattern `[A-Za-z0-9_.-]{,64}`;
non possono quindi contenere spazi.
Le directory associate ai vocabolari controllati DOVREBBERO essere in minuscolo,
mentre quelle associate alle ontologie e ai schemi DOVREBBERO essere in CamelCase.

I contenuti degli asset DEVONO essere codificati in UTF-8.

Ad esempio:

- il percorso dell’ontologia `MyOntology` sarà `assets/ontologies/MyOntology/`;
- il percorso del vocabolario `my-vocabulary` sarà `assets/controlled-vocabularies/my-vocabulary/`.

## Versionamento

**Nota: la versione attuale di NDC indicizza in maniera versionata solamente le ontologie.**

Le directory degli asset POSSONO essere avere sub-directory
per supportare il versionamento.
Il nome delle sub-directory DEVE rispettare il pattern:

`(latest|v?[0-9]+(\.[0-9]+){0,2})`.

Una directory contenente asset NON DEVE contenere contemporaneamente
sub-directory versionate con e senza il prefisso `v`
perché questo rende impossibile ordinare le versioni.

Sei esempi di path validi per le sub-directory.
Notare che le versioni dell’ontologia `Car` non sono prefissate da `v`
mentre quelle di `Person` sono tutte prefissate da `v`.

```bash
└── assets
    ├── ontologies
    │   └── Car
    │   |   ├── 1.3
    │   |   ├── 202101
    │   |   └── 4.5.6
    │   └── Person
    │       ├── v1.3
    │       └── v4.5.6
    └── schemas
        └── Person
            └── latest
```

Sei esempi di path non validi, anche perché
le directory contengono contemporaneamente
versioni prefissate da `v` che senza prefisso.

```bash
└── assets
    ├── ontologies
    │   └── MyOntology
    │       ├── v1.4-beta
    │       ├── versione 2.9
    │       ├── v4..6
    │       ├── v.3
    │       └── 4.5.
```

### File di Documentazione

Le directory degli asset POSSONO contenere file di documentazione in formato Markdown.
L’estensione del file DEVE essere `.md` (ad esempio `README.md`).
Questi file vengono ignorati durante il processamento da parte di NDC.

### Esempi

Ad esempio, analizziamo un repository strutturato come segue

```bash
┌─ README.md
├─ publiccode.yaml
|
├─ assets/ontologies/
│  ├─ Onto1/
│  │  ├─ onto1.ttl
│  │  └─ onto1.rdf
│  ├─ Onto2/
│  │  └─ README.md
│  ├─ Onto3/
│  │  ├─ Other/
│  │  │  └─ temp.md
│  │  └─ onto3.ttl
│  ├─ Onto4/
│  │  └─ latest/
│  │     ├─ onto1.ttl
│  │     └─ onto1.rdf
│  └─ notes.md
|
└─ assets/controlled-vocabularies/
   └─ ...

```

Il repository non contiene schemi, quindi NDC non aggiungerà schemi al catalogo durante l’harvesting.
Questo non rappresenta un problema e non è considerato un errore.

I file informativi (e.g. README.md, notes.md) presenti sia nella radice che
nelle sottodirectory vengono ignorati durante l’harversting.

Per quanto riguarda la directory `Onto1/`:

- essa non contiene sotto-directory né altre directory al suo interno
  ed è quindi una cartella foglia.
  Quindi viene processata come potenzialmente contenente un’ontologia;
- contiene un file RDF/Turtle che verrà processato;
- contiene un altro file RDF, plausibilmente una serializzazione diversa degli stessi contenuti del file .ttl in RDF/XML.
  Poiché NDC processa solo i file di tipo text/turtle con estensione `.ttl`, questo file viene ignorato.

La directory `Onto2/` non contiene file `.ttl`: questo viene segnalato solamente come WARNING.

La directory `Onto3/` ha una sottodirectory, quindi non è considerata come contenitore di ontologia,
ma come directory intermedia nel cammino per altre directory foglia:
il file `onto3.tll` è ignorato e non processato.

La directory `Onto4/` contiene una sottodirectory `latest/` che contiene un file `.ttl`, quindi viene processata come potenzialmente contenente un’ontologia.

```{include} ontologie.md
```

```{include} vocabolari.md
```

```{include} schemi.md
```
