# Riferimenti e sigle

## Note di lettura del documento

Conformemente alle norme ISO/IEC Directives, Part 3 per la stesura dei documenti tecnici questo documento utilizza le parole chiave "DEVE", "DEVONO", "NON DEVE", "NON DEVONO", "DOVREBBE", "NON DOVREBBE", "PUÒ" e "OPZIONALE", la cui interpretazione è descritta di seguito.

- DEVE o DEVONO, indicano un requisito obbligatorio per rispettare le Linee Guida;
- NON DEVE o NON DEVONO, indicano un assoluto divieto delle specifiche;
- DOVREBBE o NON DOVREBBE, indicano che le implicazioni devono essere comprese e attentamente pesate prima di scegliere approcci alternativi;
- PUÒ o POSSONO o l’aggettivo OPZIONALE, indica che il lettore può scegliere di applicare o meno senza alcun tipo di implicazione o restrizione la specifica.

Per compattezza, gli esempi di JSON possono essere serializzati anche in formato YAML
(vedi anche https://www.w3.org/TR/json-ld11/#data-model-overview).
E’ in corso la standardizzazione del formato [YAML-LD](https://github.com/json-ld/yaml-ld)
utile a rappresentare nel più conciso formato YAML contenuti Linked Data.

## Riferimenti normativi

- [CAD art. 50](https://www.normattiva.it/uri-res/N2Ls?urn:nir:stato:decreto.legislativo:2005-03-07;82~art50!vig=2050-01-01)

## Termini e definizioni

- Agid:
  Agenzia per l'Italia Digitale
- API:
  Application Programming Interface
- YAML:
  https://yaml.org/spec/
- Erogatore, Fruitore, e-service:
  ai sensi
  del Modello di interoperabilità delle Pubbliche Amministrazioni composto
  dalle Linee Guida emanate da Agid.
- JSON:
  RFC8259
- RDF:
  Resource Description Framework. Un framework che permette di rappresentare informazioni sul web basandosi su due
  strutture dati: grafi (insiemi di triple soggetto-predicato-oggetto) ed elementi (IRI, blank e literals);
  e su dei vocabolari di elementi identificati tramite degli IRIs e dei namespace.
  Un rdf-dataset è un insieme di grafi.
- JSON-LD 1.1:
  https://www.w3.org/TR/json-ld11/ è un formato che permette di serializzare in JSON delle informazioni basate sul [RDF modello dati RDF](https://www.w3.org/TR/json-ld11/#data-model).
  Un documento JSON-LD è quindi sia un documento  RDF che JSON, e rappresenta un'istanza di un RDF data model.
  JSON-LD inoltre *estende* RDF per permettere la serializzazione di dataset RDF generalizzati.
- Vocabolario:
  [w3c](https://www.w3.org/standards/semanticweb/ontology) Nel Semantic Web, i vocabolari definiscono i concetti e le relazioni (chiamati anche "termini") usati per descrivere e rappresentare un'area di interesse. I vocabolari possono essere molto complessi (con diverse migliaia di termini) o molto semplici (descrivendo solo uno o due concetti). I vocabolari sono gli elementi di base per le tecniche di inferenza sul web semantico.
Ontologia: una ontologia è un insieme di assiomi logici che concettualizzano un dominio di interesse definendo dei concetti e la semantica delle relazioni tra essi. Quando le ontologie contengono ulteriori restrizioni (eg. vincoli allo schema) non sono propriamente vocabolari.

```
Man ≡ Human ∩ Male
Child
Father ≡ Man ∩ ∃ hasChild.
```

- Core Vocabulary:
  un modello dati semplificato, riusabile ed estensibile che individua le caratteristiche fondamentali di un entità in modo indipendente dal contesto e dalla sintassi.

- Vocabolario controllato:
  un vocabolario dove i termini sono validati da un'autorità designata. Può essere di diversi tipi - eg. una lista (codelist), una struttura gerarchica (tassonomia), un glossario ed un tesauro (che aggiunge ad una tassonomia ulteriori vincoli). Esempi di vocabolari controllati europei si trovano qui https://op.europa.eu/en/web/eu-vocabularies/controlled-vocabularies Schema di dati: Uno schema è una rappresentazione/descrizione formale e machine-readable del contenuto effettivo o potenziale dei dati contenuti in un oggetto separato. In altre parole, è l'insieme di istruzioni semantiche e sequenziali che possono essere usate per controllare l'input memorizzato in un dato file, o per collegare un file che rispetta tali istruzioni a un sistema o un'applicazione di scambio di informazioni. Esistono diversi formati per descrivere degli schemi, tra cui xml-schema e json-schema. Definizione formale della sintassi di una entità. Vedi https://json-schema.org/understanding-json-schema/about.html
