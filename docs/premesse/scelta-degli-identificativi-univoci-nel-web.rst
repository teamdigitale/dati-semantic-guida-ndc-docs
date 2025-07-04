Scelta degli identificativi univoci nel Web 
============================================

Per individuare univocamente tutti gli elementi (entità, attributi di
entità, relazioni tra entità) che compongono le risorse semantiche che
il Contributore intende creare e registrare nel catalogo, occorre
definire degli URI/IRI persistenti nel tempo 
(rif. `manuale operativo <../manuale-operativo/identificativi-univoci-delle-risorse.html>`__).

A tal fine, il Contributore può scegliere una tra le seguenti opzioni:

- **Utilizzare il** `servizio w3id.org del W3C Permanent Identifier
  Community Group <https://w3id.org>`__, per la registrazione di identificativi permanenti a
  partire dai quali reindirizzare verso URL specifici come spiegato nel
  `manuale operativo <../manuale-operativo/identificativi-univoci-delle-risorse.html>`__.
  In questo caso le opzioni possono essere:

   *  ``w3id/<dominio_specifico>``: il Contributore avrà piena autonomia
      nella gestione degli URI. Il Consorzio di società che amministra
      w3id.org ha definito la seguente pratica: "la pratica attuale [di
      w3id.org] è quella di rivendicare un nome di directory di primo
      livello e aggiungere identificatori di secondo livello specifici
      del progetto. Non esiste un elenco o una politica ufficiale per
      gli identificatori riservati. Tuttavia, gli amministratori possono
      rifiutare richieste di identificatori troppo generici, che
      potrebbero causare confusione, inappropriati o offensivi o che
      potrebbero comunque essere necessari per future espansioni del
      servizio”. Questa soluzione è stata adottata dal 
      `progetto sui dati aperti della zootecnia italiana LEO <https://w3id.org/leo/>`__.
     
   *  ``w3id.org/italia``: il Contributore dovrà ricevere l'approvazione
      a contribuire al dominio “Italia” da parte dei relativi
      amministratori (DTD-Dipartimento per la Trasformazione Digitale)
      non dovendo, al tempo stesso, provvedere all’organizzazione dei
      reindirizzamenti; in questo caso, il Contributore beneficerà delle
      soluzioni di content negotiation e URI dereferentiation già
      incluse. La scelta del dominio ``w3id.org/italia`` comporta, inoltre,
      necessariamente l’archiviazione delle proprie risorse semantiche
      nell'`apposito repository <https://github.com/italia/dati-semantic-assets>`__
      gestito dal DTD; dunque, ogni operazione (inserimento,
      aggiornamento, modifica) da compiersi in tale repository github è
      subordinata all’approvazione dei suoi amministratori. Questa
      soluzione è stata adottata per alcune ontologie di respiro
      nazionale come l’ontologia Learning del Ministero dell’Università
      e della Ricerca o l’ontologia RPO sulla popolazione residente del
      Ministero dell’Interno.

   *  ``w3id.org/italia/<dominio_specifico>``: il Contributore dovrà
      ricevere l’approvazione degli amministratori di ``w3id.org/italia``
      (DTD – Dipartimento per la Trasformazione Digitale) per la
      denominazione degli identificatori di secondo livello, ossia la
      denominazione nelle URI del dominio specifico. La denominazione
      del dominio specifico dovrà rispettare quanto indicato nelle 
      `Linee guida open data <https://www.agid.gov.it/sites/default/files/repository_files/lg-open-data_v.1.0_1.pdf>`__
      (sezione 7.1.3 pagina 114, 115) adottata da Agid con
      Determinazione n. 183/2023. In questo caso, il contributore dovrà
      configurare e gestire in autonomia il repository che conterrà le
      risorse semantiche del proprio dominio. Ad esempio, questa
      soluzione è stata adottata da 
      `INPS <https://w3id.org/italia/social-security/>`__,
      `INAIL <https://w3id.org/italia/work-accident/>`__,
      `Regione Lombardia <https://w3id.org/italia/lombardia/>`__.
      Inoltre, il Contributore
      potrà scegliere se utilizzare la soluzione di *URI
      dereferentiation* gestita dal Catalogo, o se usare una soluzione
      gestita in autonomia, così come nel caso di 
      `ISPRA <https://w3id.org/italia/env/>`__.

- **Utilizzare URI registrate in un proprio dominio** per gestire
  autonomamente gli identificatori delle risorse semantiche da
  pubblicare su schema.gov.it: in questo caso, il Contributore
  garantisce la persistenza degli identificatori nel tempo essendo
  completamente autonomo nella gestione degli URI. Questa opzione è
  stata adottata dal 
  `Ministero della Cultura (MiC) <http://dati.beniculturali.it/cis/>`__
  nella definizione delle risorse
  semantiche dell’Ontologia Cultural-ON dei Luoghi della Cultura e
  degli Eventi Culturali.
