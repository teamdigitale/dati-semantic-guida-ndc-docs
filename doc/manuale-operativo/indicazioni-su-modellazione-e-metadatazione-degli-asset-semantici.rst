Indicazioni su modellazione e metadatazione degli asset semantici
=================================================================

Di seguito si riportano le linee guida di base per l’aggiunta di un
nuovo vocabolario controllato, una nuova ontologia e un nuovo schema
dati.

Nuovo vocabolario controllato
-----------------------------

Il vocabolario controllato è un dataset aperto e, pertanto, è metadatato
seguendo le linee guida nazionali sui dati aperti, adottando cioè il
profilo nazionale di metadatazione
`DCAT-AP_IT <https://docs.italia.it/italia/daf/linee-guida-cataloghi-dati-dcat-ap-it/it/stabile/index.html>`__
e una licenza aperta.

Nel contesto delle iniziative per promuovere le politiche di
valorizzazione del patrimonio informativo pubblico, AGID (Agenzia per
l’Italia Digitale) ha collaborato con un Gruppo di Lavoro composto da
amministrazioni centrali e locali per definire il profilo nazionale dei
metadati (DCAT-AP_IT).

Questo profilo permette la documentazione dei dati di tipo aperto nel
Catalogo, in linea con la specifica \ `DCAT-AP
(1.1) <https://joinup.ec.europa.eu/collection/semic-support-centre/solution/dcat-application-profile-data-portals-europe/release/11>`__,
definita nell’ambito del \ `programma
ISA <https://ec.europa.eu/isa2/home_en/>`__ della Commissione Europea.

È reso, dunque, disponibile da parte di AGID un `validatore di file
aderente al profilo
DCAT-AP_IT <https://portaledati3-130.dati.gov.it:3030/dcat-ap_validator.html>`__:
può essere utilizzato dal Contributore al fine di verificare il rispetto
delle specifiche in oggetto, ricordando che eventuali errori segnalati
su “dcatapit:Catalog” e su “owl:versionInfo” possono essere ignorati.

Inoltre, è necessario aggiungere al dataset il metadato ndc:keyConcept
definito nell’\ `ontologia NDC <https://w3id.org/italia/onto/NDC>`__ .
Il key concept è il concetto principale o chiave a cui il vocabolario
controllato si riferisce. Ad esempio, per il dataset
https://w3id.org/italia/controlled-vocabulary/classifications-for-public-services/authentication-type
il concetto chiave, quindi il valore della proprietà ndc:keyConcept, è
"authentication-type" (il tipo di autenticazione). Questo metadato è
necessario per abilitare i meccanismi di harvesting del catalogo
schema.gov.it

Essendo un vocabolario controllato un dataset per organizzare la
conoscenza, esso è rappresentato utilizzando lo standard web di
riferimento per i sistemi di organizzazione della conoscenza, ossia
l’ontologia `SKOS <https://www.w3.org/TR/skos-primer/>`__.

In particolare, il Contributore:

- definisce il ConceptScheme di SKOS che rappresenta tutto il
  vocabolario controllato collegandolo ai singoli concetti di primo
  livello mediante la proprietà skos:hasTopConcept. Un vocabolario
  controllato può essere infatti una lista di codici (code list), una
  tassonomia (taxonomy), oppure qualcosa di più complesso come un
  tesauro. La proprietà skos:hasTopConcept collega tutti i singoli
  concetti in una lista di codici, i concetti di primo livello negli
  altri casi più articolati;

- per ciascun concetto, inoltre, specifica le seguenti proprietà:

   * skos:notation con l’identificativo univoco associato al concetto;
   * skos:prefLabel con l’etichetta principale di riferimento per il
     concetto definita con almeno il tag in italiano. È opportuno
     aggiungere anche la lingua inglese, soprattutto se il vocabolario
     è utilizzato in un contesto di interoperabilità anche
     transfrontaliera. Si ricorda che l’etichetta che rappresenta il
     valore di questa proprietà deve essere esplicita e non contenere
     abbreviazioni di testo che la renderebbe comprensibile solo da
     parte dell’ente che propone il vocabolario. È opportuno che
     l’etichetta principale sia nella forma singolare, lasciando
     eventualmente le forme plurali in un’etichetta alternativa
     rappresentata con la proprietà skos:altLabel;
   * skos:inScheme che assume come valore l’URI del vocabolario
     controllato che si sta definendo.

- in presenza di tassonomie o tesauri indica anche i concetti di
  livello inferiore e superiore attraverso le proprietà skos:narrower e
  skos:broader nonché di quanti livelli si compone il vocabolario
  mediante la proprietà xkos:numberOfLevels, il cui valore indica il
  numero di livelli gerarchici previsti dal vocabolario controllato.

È opportuno che altre proprietà SKOS siano aggiunte ai vari concetti,
come per esempio skos:definition quando una definizione formale del
concetto è nota , skos:note per aggiungere qualsiasi altra nota, qualora
esistente.

Qualora un concetto sia allineato semanticamente in maniera più o meno
forte ad analoghi concetti definiti in altri vocabolari controllati
esistenti nel web (es. schema.org, EU authority list) è buona norma
utilizzare le proprietà skos:exactMatch (i due concetti sono di fatto la
stessa cosa), skos:relatedMatch (i due concetti sono tra loro
relazionati, nel senso più generale), skos:closeMatch (i due concetti
sono molto simili ma non esattamente la stessa cosa) al fine di creare
collegamenti tra diversi dataset dei vocabolari controllati (linked open
data).

Nuova ontologia
---------------

Nel caso di proposta di una nuova ontologia, il Contributore rispetta le
seguenti indicazioni:

-  consegnare un’ontologia che non presenta errori sintattici. Non
   saranno valutate ontologie che non riescono a essere aperte con
   successo da software di editing di ontologie come per esempio
   Protégé;

-  l’ontologia è almeno serializzata in RDF/Turtle (serializzazione
   utilizzata nella procedura di harvesting di schema.gov.it);

-  l’ontologia è metadatata attraverso l’ontologia
   `ADMS-AP_IT <https://www.schema.gov.it/semantic-assets/details?uri=https%3A%2F%2Fw3id.org%2Fitalia%2Fonto%2FADMS>`__.
   Questo profilo di metadatazione è specifico per ontologie e si basa
   su DCAT-AP_IT. È questa metadatazione che consente di abilitare
   l’harvesting dell’ontologia in schema.gov.it. Per verificare la
   correttezza della metadatazione, i Contributori avranno a
   disposizione un modulo di pre-harvesting raggiungibile da un’apposita
   pagina web, così come espresso nel workflow in 
   `Attività propedeutiche alla contribuzione al Catalogo <../come-contribuire/attività-propedeutiche-alla-contribuzione-al-catalogo.html>`__;

-  si verifica con dei ragionatori automatici, presenti come plug-in nei
   principali editor di sviluppo di ontologie come ad esempio Protégé o
   Eddy, che l’ontologia prodotta non abbia inconsistenze semantiche e
   che quello che si vuole modellare sia correttamente inferito dal
   ragionatore;

-  le classi e proprietà di ogni tipo delle ontologie sono sempre
   annotate con almeno le proprietà rdfs:label e rdfs:comment in
   italiano. Qualora l’ontologia abbia una potenzialità in un contesto
   transfrontaliero, si fornisce anche la versione in lingua inglese
   delle stesse proprietà. È opportuno inoltre specificare la proprietà
   di annotazione rdfs:isDefinedBy con l’URI dell’ontologia;

-  riutilizzare direttamente tutte le ontologie già esistenti in
   schema.gov.it qualora questo si applichi alla nuova modellazione.
   Questo consente anche di riutilizzare pattern di modellazione già
   implementati che, da letteratura scientifica, hanno dimostrato di
   fornire maggiori garanzie di interoperabilità semantica tra
   modellazioni diverse. A titolo d’esempio: se si deve definire un
   concetto di persona fisica oppure di organizzazione (pubblica o
   privata che sia) ma anche concetti legati al tempo o a ruoli di
   agenti che agiscono su oggetti del dominio è necessario riutilizzare
   rispettivamente le ontologie CPV (Persone), COV (Organizzazioni), TI
   (tempo), RO (ruoli);

-  si ricorda che il riutilizzo diretto di concetti e/o proprietà già
   esistenti comporta l'ereditarietà di tutti i vincoli di cardinalità
   (restrizioni OWL) già definiti nelle ontologie di schema.gov.it;

-  qualora ci sia necessità di aggiungere altre proprietà o vincoli di
   cardinalità a concetti già esistenti in ontologie già disponibili, o
   si richiede tale aggiunta agli Amministratori del Catalogo per agire
   direttamente nelle ontologie di schema, oppure si definisce un
   proprio concetto che potrà diventare sottoclasse del concetto già
   esistente in ontologie esistenti di schema.gov.it;

-  è raccomandato allineare la nuova ontologia all’ontologia di livello
   top nazionale l0. Questa raccomandazione ha alcuni vantaggi: 1) aiuta
   a comprendere meglio cosa si sta modellando. Se si modella un’entità
   che è “concetto” questa non può essere anche un “evento”; 2)
   l’ontologia l0 aiuta a collegare tutte le ontologie tra loro creando
   quindi una grossa rete di ontologie nazionali. Il collegamento tra
   modelli concettuali abilita il collegamento tra i dati rappresentati
   con quei modelli; 3) l0 è molto utile per verificare, attraverso
   l’inferenza semantica, eventuali inconsistenze semantiche in
   un’ottica più generale di rete più che di singola ontologia;

-  è possibile aggiungere vincoli di cardinalità mediante restrizioni
   OWL, ma è bene non vincolare troppo le varie definizioni per dare più
   possibilità di riutilizzo alle ontologie anche in altri potenziali
   contesti, visto la valenza nazionale che nuove ontologie possono
   assumere con la pubblicazione in schema.gov.it. A tal proposito si
   suggerisce di definire restrizioni OWL come sottoclassi della classe
   a cui si riferiscono così da specificare una condizione necessaria ma
   non sufficiente e valutare attentamente se il vincolo di cardinalità
   è di fatto sempre stringente (costrutti come “some”, “exactly 1”) o
   meno (“max 1”, ecc.). Qualora ci siano vincoli di cardinalità più
   stringenti dal punto di vista applicativo, è bene che il Contributore
   consideri la possibilità di rilassare alcune restrizioni OWL definite
   nell’ontologia e creare a parte un vero e proprio profilo applicativo
   mediante regole SHACL, standard web pubblicato dal W3C. Questa
   pratica, tra l’altro, è quella adottata da alcuni paesi europei (es.
   Belgio) e dalla Commissione Europea stessa nel contesto di iniziative
   di interoperabilità semantica quali i core vocabulary, l’ontologia
   ePO sul’e-procurement, l'ontologia ELM – European Learning Model;

-  è opportuno modularizzare il più possibile le ontologie, più che
   creare ontologie che contengono la rappresentazione di svariati
   domini/tipologie di dati. L’evidente vantaggio della modularizzazione
   è quello di riuscire a gestire in modo più agevole eventuali
   evoluzioni future che potrebbero anche seguire diverse frequenze di
   aggiornamento delle diverse tipologie di dato;

-  è opportuno utilizzare ontology design pattern e un approccio agile
   alla modellazione con rilasci più frequenti e definizioni di versioni
   anche instabili dell’ontologia pian piano raffinate con requisiti
   nuovi fino alla versione finale. Gli ontology design pattern sono
   soluzioni di modellazione già disponibili, riusabili ed efficaci che
   possono essere specializzati o direttamente applicati nel dominio da
   modellare e che risolvono problemi di modellazione ricorrenti (es. un
   qualcosa che cambia nel tempo). Essi aiutano a ridurre l’arbitrarietà
   nel design dell’ontologia e consentono di ridurre gli errori di
   modellazione e quindi migliorare la qualità delle ontologie. Si
   ricorda, come prima menzionato, che già le ontologie esistenti
   implementano ontology design pattern che si devono riutilizzare (es.
   ruoli nel tempo, oggetti che variano nel tempo, valori, ecc.);

-  è buona norma allineare l’ontologia anche ad altre ontologie
   esistenti nel Web dei Dati, qualora questo sia applicabile;

-  è possibile corredare l’ontologia di una rappresentazione grafica dei
   concetti e delle loro relazioni. A tale scopo i Contributori sono
   liberi di utilizzare strumenti di loro preferenza. Solo a titolo
   d’esempio si possono citare diagrammi di rappresentazione grafica che
   utilizzano la notazione `UML <http://www.uml.org/>`__, che possono
   essere prodotti con strumenti quali diagrams.net, Visual Paradigm,
   StarUML oppure che usano notazioni tecniche specifiche di disegno
   ontologico come per esempio
   `Graffoo <https://essepuntato.it/graffoo/>`__ (che è possibile
   abilitare con strumenti come
   `yEd <https://www.yworks.com/products/yed>`__ oppure
   `draw.io <https://app.diagrams.net/>`__) o
   `Graphol <https://www.diag.uniroma1.it/degiacom/papers/2022/fi2022lssd.pdf>`__
   (che è possibile utilizzare attraverso strumenti come
   `Eddy <https://github.com/obdasystems/eddy>`__).

Nuovi schemi dati
-----------------

I nuovi schemi dati devono avere un collegamento con gli asset semantici
di tipo ontologie e vocabolari controllati, qualora questi esistano in
schema.gov.it e siano pertinenti rispetto agli attributi dello schema
dati.

Gli schemi dati per essere sottoposti al processo di harvesting debbono
contenere due file: il file di metadati in formato RDF/Turtle, e il
modello dello schema dati in formato OpenAPI.

In particolare, il file di metadati deve avere l’estensione .ttl e un
nome specifico, ossia “index.ttl”.

Il file “index.ttl”, come per le ontologie, deve contenere tutti i
metadati previsti dall’ontologia
`ADMS-AP_IT <https://www.schema.gov.it/semantic-assets/details?uri=https%3A%2F%2Fw3id.org%2Fitalia%2Fonto%2FADMS>`__.
Questo profilo di metadatazione si basa su DCAT-AP_IT. È l'adozione di
questo modello che consente l'harvesting anche degli schemi dati.

Mentre il file che riporta lo schema del servizio deve avere
l'estensione .yaml (se viene utilizzata la versione 3.0 di OpenAPI si
usa oas3.yaml).

Le sezioni principali e obbligatorie all’interno del file che riporta lo
schema del servizio sono le seguenti:

- **info**: le informazioni iniziali riguardanti il titolo (title) e la descrizione (description) dello schema dati del servizio;

- **components**:

   * **schemas**: vengono descritti i concetti all’interno del
     servizio, definendo quali sono i concetti di input obbligatori
     (required). Per ogni concetto sono dichiarate le seguenti voci:
   * **type**: il tipo di dato (object, string, integer);
   * **description**: si riporta la URI del concetto di riferimento;
   * per i concetti di tipo object è necessario elencare le properties.
     Per le properties è necessario definire il tipo di dato (type): se
     si tratta di un object si riporta il riferimento al concetto,
     altrimenti è necessario riportare il tipo di format e quando
     richiesto il pattern;
   * **x-jsonld-type**: si riporta la URI del concetto di riferimento;
   * **x-jsonld-context**:

      + **‘@vocab’**: si riporta la radice della URI dell’ontologia maggiormente referenziata all’interno dello schema dati del servizio.

Si riporta un breve esempio di seguito:

::

   components:
     schemas:
       TaxCode:
         type: string
         description: https://w3id.org/italia/onto/CPV/taxCode.
         example: RSSMRA75L01H501A
         maxLength: 16
         minLength: 11
       Person:
         type: object
         description: https://w3id.org/italia/onto/CPV/Person
         x-jsonld-type: https://w3id.org/italia/onto/CPV/Person
         x-jsonld-context:
           "@vocab": https://w3id.org/italia/onto/CPV/
   	  tax_code:
   	    "@id": taxCode
   	  date_of_birth: dateOfBirth
   	  family_name: familyName 
   	  given_name: givenName     
         properties:
           tax_code:
             $ref: "#/components/schemas/TaxCode"
           date_of_birth:
             format: date
             type: string
   	    pattern: ([0-9]{4})-([0-1][0-9])-([0-3][0-9])
           family_name:
             type: string
           given_name:
             type: string
