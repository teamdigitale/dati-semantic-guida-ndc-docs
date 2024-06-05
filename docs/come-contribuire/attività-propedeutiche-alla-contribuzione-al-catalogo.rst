Attività propedeutiche alla contribuzione al Catalogo
=====================================================

Le attività propedeutiche alla contribuzione al Catalogo da parte di un
Contributore sono:

-  Effettuare un’analisi delle risorse da creare, oppure delle possibili
   proposte di modifica da effettuare per risorse già pubblicate sul
   catalogo;

-  Individuare la modalità di contribuzione più consona al caso
   specifico sulla base delle informazioni contenute nelle sotto-sezioni
   seguenti eventualmente richiedendo supporto agli Amministratori del
   Catalogo;

-  Effettuare le ulteriori azioni di competenza descritte nel seguente flowchart.

.. mermaid::
   
   flowchart TB
      classDef default stroke:white,color:#fff,clusterBkg:none,fill:#3344d0
      classDef cluster font-weight: bold,fill:none,color:darkgray,stroke:#3344d0,stroke-width:2px
      classDef subgraph_padding fill:none, stroke:none, opacity:0
      classDef bounded_context stroke-dasharray:5 5
   subgraph b["Amministratori del Catalogo"]
   id0["Analisi della richiesta di contribuzione espressa"]
   end
   subgraph Organizzazione Contributrice
   
   id1((START))--> id2["Individuazione degli asset da creare o modificare"]
   id2--> id3{"Difficoltà nel determinare la modalità"}
   id3--> |Sì|id4["Organizzazione chiede supporto per determinare la modalità più opportuna"]
   id4-.-> id0
   id3--> |No|id5["Individuazione della modalità di contribuzione"]
   id0-.->id5
   id5--> id6{"Modalità di contribuzione"}
   id6--> |Richiesta di semantic stewardship|id7["Invia richiesta di contribuzione al Catalogo utilizzando l'apposita email"]
   id6--> |Aggiornamento/Creazione asset semantici|id8["Verifica sul Catalogo di risorse semantiche correlate"]
   id8--> id9{"Presenza della risorsa"}
   id9--> |Aggiunta di nuove risorse|id30["Scelta del dominio sotto cui pubblicare"]
   id30--> id31{"Soluzione URI stabili già implementata dall'organizzazione"}
   id9--> |Modifiche a risorse già a Catalogo|id10["Apertura Issue sul repository relativo all'asset da modificare"]
   id10--> id11["Per lo sviluppo della proposta, riferirsi al Manuale Operativo"]
   direction TB
   id31--> |Sì|id15["Modellazione e metadatazione degli asset"]
   id15--> id16["Predisposizione del repository git"]
   id16-->id17["Utilizzo della propria soluzione per le URI stabili"]
   id17-->id18["Test dei requsiiti tecnici per l'harvesting degli asset semantici"]
   id31--> |No| id42["Valutazione risorse da pubblicare"]
   id42--> id43{"Tipologia risorsa"}
   id43--> |Risorse con elevato livello di generalità|id44["Riferirsi alle indicazioni nel wiki del repository nazionale"]
   id43--> |Risorse non caratterizzate da elevato livello di generalità|id46["Modellazione e metadatazione degli asset"]
   id46-->id47["Predisposizione del repository git"]
   id47-->id48["Implementazione redirect su URI stabili sotto w3id"]
   id48-->id49["Test dei requsiiti tecnici per l'harvesting degli asset semantici"]
   id49-->id50((END))
   id18-->id40((END))
   id7--> id20((END))
   id11-->id41((END))
   id44-->id45((END))
  end

Diagramma delle attività propedeutiche alla contribuzione

Aggiunta di nuove risorse
-------------------------

Di seguito il dettaglio delle attività propedeutiche del Contributore
per l’aggiunta di nuove risorse sul Catalogo:

- Se vuoi **registrare URI sotto il** ``w3id.org/italia``:

   * Nel caso in cui si abbiano a disposizione risorse da pubblicare
     caratterizzate da un elevato livello di generalità e
     riutilizzabilità su scala nazionale, allora si potranno registrare
     URI sotto ``w3id.org/italia``, beneficiando dei meccanismi di *URI
     dereferentiation* e *Content Negotiation* già implementate. A tale
     scopo, fai riferimento alle istruzioni contenute nel `repository
     Italia <https://github.com/italia/daf-ontologie-vocabolari-controllati>`__
     e alle indicazioni rese disponibili nel 
     `manuale operativo <../manuale-operativo/indicazioni-su-modellazione-e-metadatazione-degli-asset-semantici.html>`__
     su come modellare e metadatare le risorse.

   * Nel caso in cui le risorse da pubblicare non siano caratterizzate
     da un elevato livello di generalità e riutilizzabilità su scala
     nazionale, allora si potranno registrare URI sotto
     ``w3id.org/italia/<dominio_specifico>``. In tal caso, le istruzioni
     sono le seguenti:

      + Per la **modellazione e metadatazione**, fai riferimento alle
        indicazioni differenziate per tipologia di risorsa (vocabolario
        controllato, ontologia o schema dati) contenute nel `manuale operativo <../manuale-operativo/indicazioni-su-modellazione-e-metadatazione-degli-asset-semantici.html>`__;
      + Per la **predisposizione del repository**, fai riferimento alle
        indicazioni riguardo la struttura del repository da creare e
        che verrà registrato tra le sorgenti del Catalogo. I file
        richiesti, il versionamento e ulteriori dettagli sulle risorse
        semantiche sono contenute nel `manuale operativo <../manuale-operativo/istruzioni-su-come-predisporre-il-repository-in-cui-pubblicare-le-risorse-semantiche.html>`__;
      + Per **l’implementazione del redirect degli URI stabili,** fai
        riferimento alla soluzione descritta nel `manuale operativo <../manuale-operativo/identificativi-univoci-delle-risorse.html>`__;
      + Per il **test dei requisiti tecnici per l’harvesting delle
        risorse semantiche**, fermo restando che il Contributore è
        responsabile dei contenuti pubblicati nel proprio repository, è
        necessario verificare che le risorse semantiche soddisfino i
        requisiti tecnici richiesti per l’avvio della fase di
        harvesting da parte del Catalogo. Per supportare al meglio i
        Contributori in tale processo, gli Amministratori del Catalogo
        sono al lavoro su una pagina web “\ **Strumenti di
        validazione**\ ”, che suggerirà per ciascun use-case il
        validatore più consono da poter utilizzare. In particolare, (i)
        per i file ``index.ttl`` degli schemi dati e per le ontologie
        verrà indicato il validatore in fase di sviluppo da parte degli
        Amministratori del Catalogo; (ii) per i vocabolari controllati
        si potrà utilizzare il `validatore DCAT-AP_IT sviluppato da
        AGID <https://portaledati3-130.dati.gov.it:3030/dcat-ap_validator.html>`__
        ignorando eventuali warning ed errori sulla presenza della
        classe ``dcatapit:Catalog`` e sull’uso della proprietà
        ``owl:versionInfo`` quando più lingue vengono specificate per la
        proprietà. In aggiunta, verrà indicato il validatore delle
        OpenAPI (`Italian API Guidelines
        Checker <https://italia.github.io/api-oas-checker/>`__), ovvero
        per i file ``.yaml``. I controlli implementati dal validatore,
        attualmente in sviluppo da parte degli Amministratori, saranno
        un sottoinsieme di quelli eseguiti in fase di harvesting dalla
        piattaforma Catalogo; in particolare, i controlli
        verificheranno la presenza dei metadati mandatori nel file
        turtle e la validità dei prefissi rispetto alle relative
        ontologie. Infine, per un test di visualizzazione e di
        correttezza delle risorse semantiche rispetto ai requisiti
        tecnici per l’harvesting espressi nel `manuale
        operativo <../manuale-operativo.html>`__, è possibile richiedere,
        utilizzando la mail servicedesk.schema@istat.it, un primo
        aggiornamento nell’ambiente di test del Catalogo e, al termine
        della fase di test, richiedere l’harvesting in produzione.

- Se vuoi **registrare URI in domini come** ``w3id.org/<dominio_specifico>``:

   * Segui le istruzioni contenute nell’elenco al punto precedente. Per
     l’attività di implementazione del redirect su URI stabili, puoi
     far riferimento alla `guida ufficiale pubblicata dal
     w3id <https://w3id.org/>`__. Inoltre, per la creazione dei file di
     configurazione del redirect, puoi considerare **a titolo
     esemplificativo** le istruzioni contenute nel 
     `manuale operativo <../manuale-operativo/identificativi-univoci-delle-risorse.html>`__.

- Se vuoi **registrare URI in domini proprietari**:

   * Segui autonomamente tutte le specifiche richieste.

- Se vuoi **chiedere semantic stewardship a Istat**:

   * Invia una richiesta di contribuzione al Catalogo utilizzando la
     mail servicedesk-schema@istat.it.

Richiesta di modifica di risorse già in Catalogo
------------------------------------------------

Se vuoi **suggerire una modifica a un contenuto semantico già esistente
nel Catalogo,** fai riferimento al  
`manuale operativo <../manuale-operativo/indicazioni-su-aggiornamento-di-asset-semantici-esistenti.html>`__.
