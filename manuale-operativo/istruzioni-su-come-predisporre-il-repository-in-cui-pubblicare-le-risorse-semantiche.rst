Istruzioni su come predisporre il repository in cui pubblicare le risorse semantiche
====================================================================================

La sezione descrive le caratteristiche principali che è bene che i
repository gestiti dai Contributori abbiano affinché vengano
correttamente acquisiti dal Catalogo, nel caso gli stessi vogliano
contribuire offrendo risorse semantiche gestite in un repository di
propria titolarità.

Allo scopo di semplificare il controllo di qualità che i Contributori
devono effettuare sui propri repository, gli Amministratori del Catalogo
hanno reso disponibile presso il repository
https://github.com/teamdigitale/dati-semantic-cookiecutter un template
di controlli che possono essere integrati sul proprio repository,
**disattivando eventualmente alcuni hook non applicabili**, a supporto
dell’esecuzione dei controlli di qualità propedeutici alla richiesta di
iscrizione al Catalogo. Per ulteriori approfondimenti, è possibile far
riferimento al **file readme del cookiecutter**, nel paragrafo **Controlli Automatici e Test**.

I principali controlli implementati nel template sono descritti nelle
successive sotto-sezioni.

Struttura di base del repository
--------------------------------

La struttura di base del repository deve rispettare il seguente
template:

-  Ontologie: in ``assets/ontologies``;

-  Vocabolari controllati: in ``assets/controlled-vocabularies``;

-  Schemi: in ``assets/schemas``.

Contenuto del repository
------------------------

I file devono essere codificati in ``UTF-8``.

Le risorse semantiche devono essere presenti almeno nel seguente
formato:

-  Ontologie: ``RDF/Turtle`` (*media-type* ``text/turtle``) con estensione del
   file ``.ttl``;

-  Vocabolari controllati: ``RDF/Turtle`` (*media-type* ``text/turtle``) con
   estensione del file ``.ttl``;

-  Schemi dati: ``OAS3`` (``.oas3.yaml``) e ``turtle`` dei metadati (file
   ``index.ttl``).

Possono essere presenti ulteriori serializzazioni (es. ``RDF/XML``, ``JSON-LD``,
``CSV``, ...) che verranno ignorate dal processo di harvesting del Catalogo.

Possono essere presenti eventuali file di documentazione, ma solo in
formato *Markdown* (``.md``).

Nomi delle cartelle e dei file
------------------------------

I nomi di file e directory devono rispettare il seguente pattern
``\`[A-Za-z0-9\_-.]{,64}``.

Il nome di ciascun file deve corrispondere al nome della relativa
risorsa nell'URI utilizzato per referenziarla.

I nomi dei file di una directory devono corrispondere al nome della
directory che li contiene, a meno dell'estensione degli stessi.

Il controllo può essere disattivato nel caso in cui il Contributore
abbia implementato una propria soluzione per le URI stabili, oppure se
ha configurato una soluzione basata sul W3id 
(`Identificativi univoci delle risorse <../manuale-operativo/identificativi-univoci-delle-risorse.html>`__) 
che tratti opportunamente eventuali discrepanze tra nomi dei file, nomi delle
cartelle che li contengono e nomi delle risorse nelle relative URI.

Proiezioni in CSV dei vocabolari controllati
--------------------------------------------

Le directory del vocabolario controllato possono contenere una
proiezione in formato ``csv`` del vocabolario insieme ai metadati necessari
per mappare i campi del ``csv`` alle risorse presenti nel file ``rdf``.

Nel caso in cui si voglia pubblicare anche la proiezione ``csv`` per un
vocabolario controllato, questo deve avere la struttura di file piatto,
ossia riportare tutte le voci delle classificazioni dal primo livello al
livello di foglia. Occorre rispettare le seguenti regole:

- generare la proiezione possibilmente mediante strumenti come *JSON-LD framing*;

- eventuali commenti nel ``csv`` devono iniziare col carattere ``#``;

- l’header del ``csv`` ovvero la prima riga contenente i nomi delle
  colonne, deve rispettare le seguenti regole sulla base della presenza
  o meno, nella stessa directory del ``csv``, del file di metadati in un
  *frictionless data package*, annotato secondo le specifiche indicate in
  *REST API Linked Data Keywords*:

   * se presente, allora i nomi delle colonne devono essere conformi a
     quanto indicato nei metadati.
   * se non presente, i nomi delle colonne devono solo rispettare il
     seguente pattern: ``^[a-zA-Z0-9_]{2,64}$``.

- si suggerisce di creare la riga di header di vocabolari controllati
  alberati introducendo tante colonne quanti sono i livelli secondo la
  nomenclatura: ``codice_1_livello``, ``label_ITA_1_livello``,
  ``label_ENG_1_livello``, ``definizione``, ... ``codice_n_livello``,
  ``label_ITA_n_livello``, ``label_ENG_n_livello``, ``definizione``, ``NOTE`` (Dove ``n``
  rappresenta il numero di livelli della classificazione);

- le righe successive del ``csv`` devono contenere i valori delle colonne
  separati da ``,`` (virgola) e, se valori relativi a campi di tipo
  stringa, racchiusi in ``"`` (doppie virgolette).

I metadati di cui al precedente elenco devono essere espressi tramite un
file ``datapackage`` con estensione ``.json``, ``.yaml`` o ``.yml``.

Nel caso in cui le voci di un vocabolario siano già presenti in un
*repository triple store* è possibile estrarne il contenuto con una *query SPARQL* 
secondo il seguente formato:

::

   SELECT DISTINCT ?codice_1_livello ?label_1_livello_it ?label_1_livello_en ?label_1_livello_fr ?label_1_livello_de

   WHERE{

   <https://w3id.org/italia/controlled-vocabulary/territorial-classifications/countries/italy/ITA> a skos:Concept;

   skos:notation ?codice_1_livello;

   skos:prefLabel ?label_1_livello_it;

   skos:prefLabel ?label_1_livello_en;

   skos:prefLabel ?label_1_livello_fr;

   skos:prefLabel ?label_1_livello_de.

   FILTER (LANG(?label_1_livello_it) = 'it')

   FILTER (LANG(?label_1_livello_en) = 'en')

   FILTER (LANG(?label_1_livello_fr) = 'fr')

   FILTER (LANG(?label_1_livello_de) = 'de')

   }

Versionamento
-------------

Le directory degli asset possono avere sub-directory per supportare il
versionamento. Il nome delle sub-directory rispetta il pattern:
``(latest|v?[0-9]+(\.[0-9]+){0,2})``.

Una directory contenente asset non contiene contemporaneamente
sub-directory versionate con e senza il prefisso ``v`` perché questo
rende impossibile ordinare le versioni.

In `Istruzioni su come predisporre il repository <../manuale-operativo/istruzioni-su-come-predisporre-il-repository-in-cui-pubblicare-le-risorse-semantiche.html#esempi>`__ 
sono contenuti alcuni esempi di versionamento delle risorse semantiche.

Approfondimenti sugli schemi dati
---------------------------------

Gli schemi utilizzano delle directory versionate come descritto nel
corso del documento.

Gli schemi per le API vengono pubblicati in formato *OpenAPI*,
corrispondenti ad una estensione di `JSON Schema Draft
4 <https://spec.openapis.org/oas/v3.0.3#data-types>`__, incorporato
nella sezione ``#/components/schema`` del file ``OAS`` compatibilmente con
le Linee Guida per l'interoperabilità tecnica. 
L’estensione del file è ``.oas3.yaml``.

È opportuno che il file YAML contenga i riferimenti semantici descritti
nel `documento
I-D-polli-restapi-ld-keywords <https://datatracker.ietf.org/doc/draft-polli-restapi-ld-keywords/>`__
attraverso:

-  il campo custom ``x-jsonld-context`` contenente un ``@context``
   *JSON-LD* conforme alle indicazioni contenute in *JSON-LD 1.1*;

-  il campo custom ``x-jsonld-type`` contenente il riferimento ad un
   ``rdf:type``.

I metadati associati sono pubblicati solo in formato ``RDF/Turtle`` (*media
type* ``text/turtle``) in un apposito file ``index.ttl``, uno per ciascuno
schema dati. È opportuno che questo file sia generato automaticamente
dal documento *OpenAPI*.

È possibile verificare sintatticamente gli schemi forniti utilizzando
l’\ `OpenAPI Checker <https://github.com/italia/api-oas-checker>`__.

Schema bundling
~~~~~~~~~~~~~~~

Quando si pubblica un documento ``OAS`` contenente la specifica di un’API, è
utile de-referenziare ed accorpare in un unico file tutti i riferimenti
a schemi ed operazioni.

Questo processo viene detto
`bundling <https://json-schema.org/understanding-json-schema/structuring.html#bundling>`__.

Il prodotto sarà un singolo ``OAS document`` (es. un file ``YAML``) utile alla
validazione sintattica e semantica dell’API.

Questo meccanismo permette di inserire nell'``IDL`` tutte le informazioni
semantiche necessarie a descrivere l’API in base sia ai riferimenti
ontologici che agli schemi utilizzati.

In `Istruzioni su come predisporre il repository <../manuale-operativo/istruzioni-su-come-predisporre-il-repository-in-cui-pubblicare-le-risorse-semantiche.html#esempi>`__
verrà fornito un caso specifico per illustrare in dettaglio il processo
di *bundling*.

Schemi XSD
~~~~~~~~~~

Attualmente il materiale semantico pubblicato dalla UE si basa sui
formati ``RDF`` ed ``XSD``.

Il Catalogo non supporta il processamento di file ``.xsd``. Questi potranno essere
supportati in un secondo momento.

In `Istruzioni su come predisporre il repository <../manuale-operativo/istruzioni-su-come-predisporre-il-repository-in-cui-pubblicare-le-risorse-semantiche.html#esempi>`__ verrà fornito un caso specifico per
illustrare in dettaglio uno *schema XSD*.

Esempi
------

Repository
~~~~~~~~~~

Ad esempio, analizziamo un repository strutturato come segue:

::

   bash
   ┌─ README.md
   ├─ publiccode.yaml
   |
   ├─ assets/ontologies/
   │ ├─ Onto1/
   │ │ ├─ onto1.ttl
   │ │ └─ onto1.rdf
   │ ├─ Onto2/
   │ │ └─ README.md
   │ ├─ Onto3/
   │ │ ├─ Other/
   │ │ │ └─ temp.md
   │ │ └─ onto3.ttl
   │ ├─ Onto4/
   │ │ └─ latest/
   │ │   ├─ onto1.ttl
   │ │   └─ onto1.rdf
   │ └─ notes.md
   |
   └─ assets/controlled-vocabularies/
     └─ ...

Il repository non contiene schemi, quindi il Catalogo non aggiungerà schemi al
catalogo durante l’harvesting. Questo non rappresenta un problema e non
è considerato un errore.

I file informativi (es. ``README.md``, ``notes.md``) presenti sia nella radice
che nelle sottodirectory vengono ignorati durante l’harversting.

Per quanto riguarda la directory ``Onto1/``:

-  essa non contiene sotto-directory né altre directory al suo interno
   ed è quindi una cartella foglia. Quindi viene processata come
   potenzialmente contenente un’ontologia;

-  contiene un file ``RDF/Turtle`` che verrà processato;

-  contiene un altro file ``RDF``, plausibilmente una serializzazione
   diversa degli stessi contenuti del file ``.ttl`` in ``RDF/XML``. Poiché il
   processo di harvesting di schema utilizza solo i file di tipo
   ``text/turtle`` con estensione ``.ttl``, questo file non è usato nel
   processo stesso.

La directory ``Onto2/`` non contiene file ``.ttl``: questo viene
segnalato solamente come **WARNING**.

La directory ``Onto3/`` ha una sottodirectory, quindi non è considerata
come contenitore di ontologia, ma come directory intermedia nel cammino
per altre directory foglia: il file ``onto3.ttl`` è ignorato e non
processato.

La directory ``Onto4/`` contiene una sottodirectory ``latest/`` che
contiene un file ``.ttl``, quindi viene processata come potenzialmente
contenente un’ontologia.

Versionamento directory degli asset semantici
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A titolo di esempio, di seguito è fornita una possibile organizzazione
delle directory sfruttando il versionamento. È importante notare che le
versioni dell’ontologia **Car** non sono prefissate da ``v`` mentre
quelle di **Person** sono tutte prefissate da ``v``.

::

   bash
   └── assets
     ├── ontologies
     │  └── Car
     │  |  ├── 1.3
     │  |  ├── 202101
     │  |  └── 4.5.6
     │  └── Person
     │    ├── v1.3
     │    └── v4.5.6
     └── schemas
       └── Person
         └── latest

Nell’esempio di seguito, invece, sono presenti sei esempi di percorsi non
validi, anche perché le directory contengono contemporaneamente versioni
prefissate da ``v`` che senza prefisso.

::

   bash
   └── assets
     ├── ontologies
     │  └── MyOntology
     │    ├── v1.4-beta
     │    ├── versione 2.9
     │    ├── v4..6
     │    ├── v.3
     │    └── 4.5.

È possibile che un repository contenga versioni precedenti delle risorse
semantiche per fini storici, al di là del versionamento supportato da
git.

L’harvesting delle ontologie considera che le directory che contengono
ontologie possano essere versionate, non i singoli file. Questo vale
anche per le sotto-directory.

Attualmente, il Catalogo non prende in considerazione il versionamento
delle cartelle per schemi dati e vocabolari controllati, ma per le
ontologie prende in considerazione:

- ``latest/`` se presente;

- quella maggiore secondo il seguente ordinamento:

   * tra due versioni espresse come forme numeriche (con punti), si
     segue l’ordinamento comunemente condiviso per cui i numeri a
     sinistra sono i più significativi;
   * qualora due versioni abbiano lunghezza diversa ma una sia prefisso
     dell’altra, la più lunga viene considerata più recente; ad
     esempio, ``v4.5`` è considerata obsoleta in presenza di ``v4.5.2``.

Focus su alberatura per le ontologie
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Di seguito viene fornito un esempio di alberatura, comprensiva di
versionamento, contenente i file che definiscono un’ontologia. In questo
caso viene processata solo la directory 'latest/'. Nell’esempio,
l’alberatura contiene una serie di file di documentazione opzionali che
non vengono processati.

::

   bash
   assets/
    ontologies/
     MyOntology/
      CHANGELOG.md
      README.md
      v1.2/
       MyOntology.ttl
       MyOntology.rdf
      v1.1/
       MyOntology.ttl
      latest/
       MyOntology.ttl
       MyOntology.rdf
       LATEST.md

Focus su alberatura per i vocabolari controllati
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Di seguito l’esempio di un’alberatura contenente un vocabolario
controllato e la sua proiezione in formato ``csv`` generata utilizzando le
informazioni di *framing* indicate in ``framing.yamlld``.

Il file ``datapackage.yaml`` contiene i metadati del ``csv``.

::

   bash
   assets/
    controlled-vocabulary/
     my-codelist/
      CHANGELOG.md
      README.md
      my-codelist.ttl
      my-codelist.csv
      datapackage.yaml
      framing.yamlld

Il file ``my-codelist.ttl`` contiene il vocabolario controllato in formato
``RDF/Turtle``.

::

   turtle

   @prefix skos: <http://www.w3.org/2004/02/skos/core#> .

   @prefix at: <http://publications.europa.eu/ontology/authority/> .

   @prefix atold: <http://publications.europa.eu/resource/authority/> .

   @prefix dc: <http://purl.org/dc/elements/1.1/> .

   @prefix owl: <http://www.w3.org/2002/07/owl#> .

   @prefix c: <http://publications.europa.eu/resource/authority/country/> .

   c:ITA a skos:Concept;

    dc:identifier "ITA";

    skos:prefLabel "Italy"@en, "Italia"@it, "Italie"@fr;

    skos:inScheme atold:country

   .

   c:DEU a skos:Concept;

    dc:identifier "DEU";

    skos:prefLabel "Germany"@en, "Germania"@it, "Allemagne"@fr;

    skos:inScheme atold:country

   .

   c:ESP a skos:Concept;

    dc:identifier "ESP";

    skos:prefLabel "Spain"@en, "Spagna"@it, "Espagne"@fr;

    skos:inScheme atold:country

   .

Il ``my-codelist.csv`` contiene le proiezioni del vocabolario controllato in
formato ``csv``.

::

   csv

   # It is possible to add comments

   #  metadata is into datapackage.yaml

   "id","label_en","label_it","label_fr"

   "ITA","Italy","Italia","Italie"

   "DEU","Germany","Germania","Allemagne"

   "ESP","Spain","Spagna","Espagne"

Il file ``Datapackage.yaml`` contiene tutte le informazioni sui metadati del
file ``csv``.

::

   yaml

   # Datapackage.yaml

   profile: data-package

   resources:

    - name: my-codelist

     path: my-codelist.csv

     profile: tabular-data-resource

     dialect:

      delimiter: ","

      doubleQuote: true

      lineTerminator: ""

     schema:

      x-jsonld-type: skos:Concept

      x-jsonld-context:

       "@context":

        skos: http://www.w3.org/2004/02/skos/core#

        dc: http://purl.org/dc/elements/1.1/

        at: http://publications.europa.eu/ontology/authority/

        atold: http://publications.europa.eu/resource/authority/

        c: http://publications.europa.eu/resource/authority/country/

        id: dc:identifier

        label_it:

         "@id": skos:prefLabel

         "@language": it

        label_en:

         "@id": skos:prefLabel

         "@language": en

        label_fr:

         "@id": skos:prefLabel

         "@language": fr

      fields:

       - name: id

        type: string

       - name: label_en

        type: string

       - name: label_it

        type: string

       - name: label_fr

        type: string

.. _schema-bundling-1:

Schema bundling
~~~~~~~~~~~~~~~

Un esempio di file ``OAS3`` metadatato con i campi ``x-jsonld-context`` e
``x-jsonld-type``:

::

   yaml

   openapi: 3.0.1

   ...

   components:

    schemas:

     Person:

      type: object

      x-jsonld-type: "https://w3id.org/italia/onto/CPV/Person"

      x-jsonld-context:

       "@vocab": "https://w3id.org/italia/onto/CPV/"

       nome_proprio: givenName

       cognome: familyName

      properties:

       nome_proprio: {type: string, ..}

       cognome: {type: string, ..}

      ...

Di seguito l’esempio di un’alberatura contenente uno schema.

::

   bash
   assets/
    schemas/
     Person/
      CHANGELOG.md
      README.md
      person.oas3.yaml
      index.ttl

.. _schemi-xsd-1:

Schemi XSD
~~~~~~~~~~

L’esempio di seguito fa riferimento al **Countries Authority Table**.

L'*authority table* dei paesi *Countries* viene pubblicata a partire
dall'URL su http://publications.europa.eu/resource/dataset/country
contenente i link a tutti i dataset associati e corrispondente al suo
URI.

All'indirizzo https://publications.europa.eu/resource/authority/country
si trova l'elenco dei paesi in formato ``RDF``; sotto quell'URL ci sono i
riferimenti ai singoli paesi, eg.
https://publications.europa.eu/resource/authority/country/ITA.

Il versionamento è contenuto all'interno degli ``RDF`` e l'URL viene
dereferenziato all'ultima versione.

Gli URI sono versionati, ad esempio
http://publications.europa.eu/resource/expression/country/20170920-0.

Da lì è possibile individuare una lista di dataset associati ed
eventualmente localizzati: qui
https://publications.europa.eu/resource/cellar/07ed8d46-2b56-11e7-9412-01aa75ed71a1.0001.12/DOC_14
la lista delle coppie codice/paese in italiano in formato ``XML`` (ATTO
table, usate per le traduzioni).

::

   xml

   <TABLE VL="IT" NAME="countries">

    <LIBELLE CODE="1A0">Kosovo</LIBELLE>

    <LIBELLE CODE="ABW">Aruba</LIBELLE>

    <LIBELLE CODE="AFG">Afghanistan</LIBELLE>

   ...

   </TABLE>

Qui una codelist (estensione ``.gc``)
http://publications.europa.eu/resource/distribution/country/20210616-0/xml/gc/Country.gc
contenente tutti i dati in un formato ``xml`` analogo a quello tabellare.

::

   xml

   <?xml version="1.0" encoding="UTF-8"?>

   <gc:CodeList xmlns:gc="http://docs.oasis-open.org/codelist/ns/genericode/1.0/">

     <Identification>

      <CanonicalUri>http://publications.europa.eu/resource/dataset/country</CanonicalUri>

   <CanonicalVersionUri>http://publications.europa.eu/resource/dataset/country/20210616-0</CanonicalVersionUri>

   <LocationUri>http://publications.europa.eu/resource/distribution/country/20210616-0/xml/gc/Country.gc</LocationUri>

     </Identification>

     <ColumnSet>

      <Column Id="code" Use="required">

        <ShortName>Code</ShortName>

        <Data Type="normalizedString" Lang="eng"/>

      </Column>

      <Column Id="Name" Use="optional">

        <ShortName>Name</ShortName>

        <Data Type="string" Lang="eng"/>

      </Column>

      <Column Use="optional" Id="ita_label">

        <ShortName>engLabel</ShortName>

        <Data Type="string" Lang="ita"/>

      </Column>

     ...

     </ColumnSet>

     <SimpleCodeList>

      <Row>

        <Value ColumnRef="code">

         <SimpleValue>ITA</SimpleValue>

        </Value>

        <Value ColumnRef="Name">

         <SimpleValue>Italy</SimpleValue>

        </Value>

        <Value ColumnRef="ita_label">

         <SimpleValue>Italy</SimpleValue>

        </Value>

     ...

     <SimpleCodeList>

Gli stessi dati possono essere recuperati a partire da
https://data.europa.eu/data/datasets/country.
