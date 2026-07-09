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

-  Effettuare le ulteriori azioni di competenza descritte nei seguenti flowchart.

.. mermaid::
   
  flowchart TB

    subgraph b["Amministratori del Catalogo"]
    id0("Analisi della richiesta di<br/> contribuzione espressa")
    end

    subgraph Contributore
    id1([START])--> id2("Individuazione degli asset<br/> da creare o modificare")
    id2--> id3{"Difficoltà <br/>nel determinare<br/> la modalità"}
    id3--> |SI|id4("Contributore chiede supporto <br/>per determinare la modalità<br/> più opportuna")
    id4-.-> id0
    id3--> |NO|id5("Individuazione della<br/> modalità di contribuzione")
    id0-.->id5
    id5--> id6{"Modalità di<br/> contribuzione"}
    id6--> |Richiesta di semantic stewardship|id7("Invia richiesta di contribuzione<br/> al Catalogo utilizzando l'apposita<br/> casella mail")
    id7--> id10([END])
    id6--> |Aggiornamento/creazione<br/> asset semantici|id8("Verifica sul Catalogo di risorse<br/> semantiche correlate")
    id8--> id9("Valutazione della presenza<br/> della risorsa a Catalogo")
    id9--> id12((A))
    end
        classDef default stroke:white,color:#fff,clusterBkg:none,fill:#0066CC
        classDef cluster font-weight:bold, font-size: 11px, fill:none, color:black, stroke:#0066CC, stroke-width:1px
        classDef subgraph_padding fill:none, stroke:none, opacity:0 
        classDef bounded_context stroke-dasharray:5 5
        linkStyle 2 stroke-width:1px,fill:none,stroke:black, font-size:11px
        linkStyle 4 stroke-width:1px,fill:none,stroke:black, font-size:11px
        linkStyle 7 stroke-width:1px,fill:none,stroke:black, font-size:11px
        linkStyle 9 stroke-width:1px,fill:none,stroke:black, font-size:11px
        class id0,id2,id4,id5,id7,id8,id9,id10 defaultNode
        classDef defaultNode font-size:11px, fill:#0066CC
        class id1,id10 startEndNode
        classDef startEndNode font-size:11px, fill:#d1e7ff, font-weight:bold, color:black
        class id3,id6 decisionNode
        classDef decisionNode font-size:11px, fill:#5a6772, color:white
        class id12 reference
        classDef reference font-size:14px, fill:#00c5ca, font-weight:bold, color:black

Diagramma 1 delle attività propedeutiche alla contribuzione

Il seguente diagramma mostra le ulteriori attività necessarie per poter aggiornare/creare asset semantici:

.. mermaid::

  flowchart TB

  subgraph Contributore
   id12((A))
   id12--> |Aggiunta di nuove risorse|id30("Scelta del dominio <br/>in cui pubblicare")
   id30--> id31{"Soluzione URI stabili<br/> già implementata<br/> dal Contributore"}
   id12--> |Modifiche a risorse<br/> già in Catalogo|id10("Apertura Issue sul repository<br/> relativo all'asset da modificare")
   id10--> id11("Per lo sviluppo della proposta<br/> riferirsi al Manuale Operativo")
   direction TB
   id31--> |SI|id15("Modellazione e metadatazione<br/> degli asset")
   id15--> id16("Predisposizione del<br/> repository git")
   id16-->id17("Utilizzo della propria soluzione<br/> per le URI stabili")
   id17-->id18("Test dei requisiti tecnici<br/> per l'harvesting degli asset semantici")
   id31--> |NO| id42("Valutazione risorse da pubblicare")
   id42--> id43{"Tipologia risorsa"}
   id43--> |Risorse con elevato<br/> livello di generalità|id44("Riferirsi alle indicazioni nel wiki<br/> del repository nazionale")
   id43--> |Risorse non caratterizzate da<br/> elevato livello di generalità|id46("Modellazione e metadatazione<br/> degli asset")
   id46-->id47("Predisposizione del  repository git")
   id47-->id48("Implementazione redirect su <br/>URI stabili sotto w3id")
   id48-->id49("Test dei requisiti tecnici<br/> per l'harvesting degli asset semantici")
   id49-->id50([END])
   id18-->id40([END])
   id11-->id41([END])
   id44-->id45([END])
  end
        classDef default stroke:white,color:#fff,clusterBkg:none,fill:#0066CC
        classDef cluster font-weight:bold, font-size: 11px, fill:none, color:black, stroke:#0066CC, stroke-width:1px
        classDef subgraph_padding fill:none, stroke:none, opacity:0 
        classDef bounded_context stroke-dasharray:5 5
        linkStyle 0 stroke-width:1px,fill:none,stroke:black, font-size:11px
        linkStyle 2 stroke-width:1px,fill:none,stroke:black, font-size:11px
        linkStyle 4 stroke-width:1px,fill:none,stroke:black, font-size:11px
        linkStyle 8 stroke-width:1px,fill:none,stroke:black, font-size:11px
        linkStyle 10 stroke-width:1px,fill:none,stroke:black, font-size:11px
        linkStyle 11 stroke-width:1px,fill:none,stroke:black, font-size:11px
        class id9,id10,id11,id15,id16,id17,id18,id30,id42,id44,id46,id47,id48,id49 defaultNode
        classDef defaultNode font-size:11px, fill:#0066CC
        class id50,id40,id41,id45 startEndNode
        classDef startEndNode font-size:11px, fill:#d1e7ff, font-weight:bold, color:black
        class id31,id43 decisionNode
        classDef decisionNode font-size:11px, fill:#5a6772, color:white
        class id12 reference
        classDef reference font-size:14px, fill:#00c5ca, font-weight:bold, color:black

Diagramma 2 delle attività propedeutiche alla contribuzione

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
     Italia <https://github.com/italia/dati-semantic-assets>`__
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
        utilizzando la mail info@schema.gov.it, un primo
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
     mail info@schema.gov.it.

Richiesta di modifica di risorse già in Catalogo
------------------------------------------------

Se vuoi **suggerire una modifica a un contenuto semantico già esistente
nel Catalogo,** fai riferimento al  
`manuale operativo <../manuale-operativo/indicazioni-su-aggiornamento-di-asset-semantici-esistenti.html>`__.
