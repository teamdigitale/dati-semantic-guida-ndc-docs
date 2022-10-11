# FAQ

1. Cos’è l’interoperabilità semantica?

   L'interoperabilità semantica è la capacità di garantire che il formato e il significato delle informazioni scambiate siano preservati e compresi durante gli scambi tra le parti.

1. Che cos’è il catalogo nazionale per l’interoperabilità semantica?

   E’ un catalogo previsto dall’investimento 1.3.1 del Piano Nazionale di Ripresa e Resilienza che contiene ontologie, vocabolari controllati e schemi dati della pubblica amministrazione italiana accessibile a chiunque voglia consultare o utilizzare degli asset semantici per sviluppare servizi digitali semanticamente e sintatticamente coerenti.

1. A chi è rivolto il catalogo?

   Il catalogo è rivolto a tutti gli enti della pubblica amministrazione ed ai privati che vogliono ricercare, consultare e utilizzare asset semantici ed in particolare agli sviluppatori di servizi digitali ed agli esperti di semantica.

1. A cosa serve e quali sono le sue funzionalità?

   Il catalogo serve a ricercare, consultare e riutilizzare ontologie, vocabolari controllati e schemi dati. In particolare è rivolto a quegli enti che creano servizi digitali basati su API di altri enti per poter riutilizzare direttamente sia i modelli semantici che i vocabolari controllati esposti dal catalogo.

   Le sue funzionalità principali sono:

   - Harvesting: automaticamente scarica gli asset semantici dai repository ufficiali pubblicati dai vari enti;
   - Ricerca: permette di ricercare e consultare assets semantici tramite una semplice web UI;
   - Consultazione: espone API REST per la ricerca e per la lettura dei vocabolari controllati ed espone [uno SPARQL endpoint](https://www.schema.gov.it/sparql) per la ricerca di ontologie.

   Inoltre, è ancora in fase di sviluppo una funzionalità di validazione della semantica e della sintassi delle API REST rispetto ai contenuti semantici pubblicati nel catalogo.

1. Quali problemi risolve il catalogo?

   Il catalogo risolve dei problemi di scalabilità, riuso, interpretazione, cultura e creazione di nuovi servizi legati all’interoperabilità semantica.

   - Scalabilità: Ogni nuovo servizio richiede lo sviluppo di codice ad-hoc per validare, interpretare ed uniformare i dati ricevuti da enti diversi e l’interazione tra enti per verificare il significato e il contesto dei dati non è scalabile;
   - Riuso degli schemi. Gli schemi dati non sono condivisi e quindi non sono facilmente riutilizzabili (né gli schemi, né il codice collegato);
   - Interpretazione dei dati. Il significato dei dati scambiati è ambiguo e spesso lasciato a interpretazione, con il rischio di inconsistenze anche sintattiche nei vari dataset e le API non sono semanticamente e sintatticamente Interoperabili;
   - Cultura della semantica. Le barriere all’ingresso per l’interoperabilità semantica sono alte;
   -Creazione di nuovi servizi. Risulta difficile creare nuovi servizi se i dati scambiati non hanno un significato chiaro (ad esempio se si confonde il nucleo familiare con la famiglia anagrafica, o un tampone molecolare con uno rapido).

1. Qual è un caso d’uso di esempio?

   Il catalogo può semplificare ed uniformare la creazione e la gestione della modulistica online e dei servizi digitali fruibili anche tramite siti web. Ad esempio, un comune invece di ridefinire i possibili titoli di studio e la loro sintassi, potrà riusare tramite API i valori pubblicati dal catalogo a partire dal vocabolario nazionale education-level.csv.

1. Chi pubblica i contenuti? I dati provengono da fonti ufficiali?

   Il cuore del catalogo è costituito da [OntoPiA](https://github.com/italia/daf-ontologie-vocabolari-controllati),
   la rete di ontologie e vocabolari controllati sviluppati nell'ambito delle azioni previste dal piano triennale per l'informatica della Pubblica Amministrazione.
   Oltre ad OntoPiA, il Catalogo permetterà la pubblicazione di asset semantici da parte di altri enti.
   Le ontologie, i vocabolari controllati e gli schemi dati sono scaricati dai repository ufficiali (e.g. Github o Gitlab) degli enti della pubblica amministrazione.
   Il catalogo scarica i dati contenuti nella directory che ha subito l'aggiornamento più recente.
   I dati provengono da fonti ufficiali in quanto ogni ente è titolare dei metadati pubblicati. L'aggiornamento dei dati è responsabilità degli enti.

   ```{mermaid}
   flowchart TB
      classDef default stroke:white,color:#fff,clusterBkg:none,fill:#3344d0
      classDef cluster font-weight: bold,fill:none,color:darkgray,stroke:#3344d0,stroke-width:2px
      classDef subgraph_padding fill:none, stroke:none, opacity:0
      classDef bounded_context stroke-dasharray:5 5

      subgraph schema.gov.it
      subgraph pad
         Ontopia
         Altri
      end
      end
      subgraph Altri
         Ente1
         Ente2
      end

      subgraph Ontopia
         o0[Ontologie ]
         v0[Vocabolari]
         s0[Schemi ]
            end

      subgraph Ente1 [...]
         o1[Ontologie ]
         v1[Vocabolari]
         s1[Schemi ]
      end

      subgraph Ente2 [Ente]
         o2[Ontologie ]
         v2[Vocabolari]
         s2[Schemi ]
      end

      %% layout
      Ente2 --- Ente1
      linkStyle 0 stroke:none
      class Altri bounded_context
      class pad subgraph_padding
   ```

1. I dati contenuti rispettano le norme vigenti sulla privacy?

   I dati contenuti e pubblicati sul catalogo sono asset semantici e per definizione non contengono dati sensibili ma solo metadati.
   Di conseguenza, i dati sono distribuiti in formato open e con licenza aperta  CC-BY 4.0. Qualsiasi dato pubblicato nel catalogo è anche disponibile nei repository resi pubblici dagli enti.

1. Il catalogo nazionale è open source? Come posso contribuire al suo sviluppo?

   Si, le componenti di frontend e backend del catalogo sono open source ed accessibili nei seguenti repository:

   - https://github.com/teamdigitale/dati-semantic-backend
   - https://github.com/teamdigitale/dati-semantic-frontend
   - https://github.com/teamdigitale/dati-semantic-kubernetes

   Trovi anche repository per la documentazione e la pubblicazione di asset semantici:

   - https://github.com/teamdigitale/dati-semantic-cookiecutter
   - https://github.com/teamdigitale/dati-semantic-guida-ndc-docs

   Inoltre c'è il repository di Ontopia, il framework di ontologie e vocabolari controllati nazionale:

   - https://github.com/italia/daf-ontologie-vocabolari-controllati

   Puoi contribuire al miglioramento del catalogo aprendo un issue in uno dei repository menzionati.

1. Come faccio ad utilizzare il catalogo?

   Per consultare il catalogo non serve autenticazione: chiunque voglia consultare degli asset semantici lo può fare tramite web UI all'indirizzo https://schema.gov.it.
   Inoltre, chiunque voglia scaricare i dati in modalità machine to machine potrà usare le API REST (per quanto riguarda i vocabolari controllati) oppure lo [SPARQL endpoint](https://www.schema.gov.it/sparql) (per interrogare le ontologie).

1. Sono un ente che gestisce dei vocabolari controllati: devo pubblicarli tutti su NDC?

   I vocabolari che contengono informazioni utili in più domini organizzativi (e.g. l’elenco delle unità amministrative, ...)
   che variano limitatamente nel tempo, dovrebbero essere pubblicati su NDC attraverso il processo descritto nella guida allo sviluppo.
   Delle code-list che sono specifiche di un dominio, ad esempio le enumeration di una specifica API del dominio fiscale che vengono
   aggiornate trimestralmente, dovrebbero invece essere pubblicate tramite un'API specifica dall’Erogatore.

1. Le ontologie servono veramente?

   Quando un servizio digitale richiede la cooperazione di più enti, è necessario accordarsi sul significato
   e la forma dei dati scambiati. Questi accordi possono avvenire bilateralmente o multilateralmente.
   Le ontologie sono una forma di accordo multilaterale, in cui gli enti si accordano preventivamente
   e dove i problemi semantici sono aggravano lo strato tecnico, rendendolo più efficiente e sicuro da mantenere.

```{mermaid}
   flowchart
    classDef default stroke:white,color:#fff,clusterBkg:none,fill:#3344d0
    classDef cluster font-weight: bold,fill:none,color:darkgray,stroke:#3344d0,stroke-width:2px
    classDef subgraph_padding fill:none, stroke:none, opacity:0
    classDef bounded_context stroke-dasharray:5 5
subgraph No Ontologies[No ontologies: n*n interaction]
A((A))
B((B))
C((C))
D((D))
E((E))
end
A <--> B & C & D & E
B <--> C & D & E
C <--> D & E
D <--> E

subgraph O[Ontologies: n+1 interactions]
direction TB
A1
B1
Ontologies <--> A1((A1)) & B1((B1)) & C1((C1)) & D1((D1)) & E1((E1))
end
```
