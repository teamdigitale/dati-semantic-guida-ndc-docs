# Introduzione alla semantica

Questa sezione introduce il tema della semantica nella creazione dei servizi digitali
ad un pubblico generico di sviluppatori web con conoscenze di tecnologie quali JSON e OpenAPI.
Contiene un sunto basato sui seguenti documenti e riferimenti:

- [Presentazione sulla semantica delle API](https://docs.google.com/presentation/d/16-u3nN0NuXQRJIxbhpPpHweijEC7eQ3fUaXftIZEGFg/)
- [REST API Linked Data Keywords](https://datatracker.ietf.org/doc/draft-polli-restapi-ld-keywords/)
  Specifiche per metadatare semanticamente API REST
- [teamdigitale/dati-semantic-guida-ndc-docs](https://github.com/teamdigitale/dati-semantic-guida-ndc-docs)
  Guida sviluppatori per risorse semantiche ed utilizzo di NDC (in fieri)
- [teamdigitale/dati-semantic-cookiecutter](https://github.com/teamdigitale/dati-semantic-cookiecutter)
  Template repository per risorse semantiche, da usare per alimentare NDC
- [schema.gov.it](https://www.schema.gov.it) il portale NDC nella sua versione attuale
- [SparQL di schema.gov.it](https://www.schema.gov.it/sparql)

## Cos’è la semantica?

La strategia digitale italiana vuole uniforme le API prodotte da migliaia di agenzie pubbliche.
Tutte queste API devono essere semanticamente interoperabili, cioè devono essere basate su un insieme ben definito di concetti.

La semantica è lo studio del significato e garantisce che venga compreso un messaggio

Prendiamo questo messaggio API: è un nome proprio o un nome completo?
Qual è il nome proprio? E ancora: il reddito in che valuta è espresso?

```yaml
{ name: "FABIANO Romildo", income: 4000000 }
```

Non possiamo fare mash-up di API con diversi formati e significati.

Nel settore pubblico, è ancora più complesso perché il significato di
un termine (ad es. "Famiglia") dipende dalle normative specifiche (ad es. Famiglia fiscale,
Famiglia registrata, ...).

I vocabolari controllati sono uno strumento di informatica che utilizza
gli URI per disambiguare il significato dei termini:
ogni termine è identificato da un URI, contestualizzato dal nome del vocabolario
che indica il dominio dei termini.

Il prefisso identifica il nome del vocabolario

```
https://dbpedia.org/data/      Dog       'The dog is a four leg animal'
--------------------------  ----------   ------------------------------
vocabulary name (prefix)       term       definition (rdfs:comment)
```

Esistono dei vocabolari standard a livello globale che contengono termini
utili a definire ulteriori vocabolari:

- [RDF](https://www.w3.org/TR/rdf-concepts/)
- [RDFS](https://www.w3.org/TR/rdf-schema/)
- [OWL](https://www.w3.org/TR/owl/)
- [SKOS](https://www.w3.org/TR/skos/)

L'Italia e l'Europa pubblicano inoltre ulteriori vocabolari ufficiali utili a creare servizi digitali.
Questi vocabolari possono anche descrivere in modo molto dettagliato dei dataset,
come il vocabolario UE [Countries](https://publications.europa.eu/resource/authority/country/)
esemplificato in un estratto:

```turtle
@prefix dc: <http://purl.org/dc/elements/1.1/> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix skos: <http://www.w3.org/2004/02/skos/core#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<http://publications.europa.eu/resource/authority/country/ITA> a euvoc:Country,
        skos:Concept ;
    dc:identifier "ITA" ;
    euvoc:euroCurrencyAdoptionDate "1999-01-01"^^xsd:date ;
    skos:prefLabel "Итaлия"@bg,
        "Italia"@eu,
        "Italia"@it
.

...
```

## Rendere la semantica accessibile

Chi sviluppa servizi web di solito non conosce i meccanismi e gli standard del web semantico
(e.g. RDF, JSON-LD, ...). D'altro canto chi si occupa di semantica non conosce le problematiche
legate alla creazione e all'operatività dei servizi digitali (e.g. scalabilità, performance, ...).
Questo fa sì che:

- le classi semantiche non siano sempre adatte a modellare gli schemi dati
  concretamente usati per scambiare efficientemente informazioni tra servizi web;
- i formati dei dati usati negli scambi possano essere inutilmente concisi o prematuramente ottimizzati,
  a scapito della chiarezza, dell'interoperabilità e della flessibilità (ad esempio definendo formati binari posizionali
  che potrebbero invece essere sostituiti da specifici meccanismi per la serializzazione quali [CBOR](https://cbor.io) e [BSON](https://bsonspec.org/)).

Ad esempio, il vocabolario Countries descritto in precedenza non è particolarmente
semplice da usare in un'API o per compilare un modulo web.
Un'API potrebbe preferire una versione sintetica dell'oggetto [Italia](http://publications.europa.eu/resource/authority/country/ITA)
da poter mappare alla bisogna sul vocabolario controllato.

```json
{ "id": "ITA",
  "label": "Italia",
  "label_en": "Italy",
  "euro_since": "1999-01-01" }
```

Pubblicare vocabolari in formati che sono ben noti
agli sviluppatori web come JSON e CSV facilita il loro utilizzo
e migliora la qualità complessiva dei dati.

Ad esempio, è possible processare il vocabolario degli Stati ed erogarlo sotto forma di CSV,
JSON o addirittura JSON Schema, in modo che possano essere utilizzato in delle API o per un modulo online.

```{mermaid}
    C4Context
      title Semantics and Technical Interoperability
      Enterprise_Boundary(s0, "Semantics") {
        System(NDC, "RDF Ontologies<br>and Vocabularies")
      }
      Enterprise_Boundary(a0, "Technical (API, Web)") {
        System(JSON, "JSON")
        System(OAS, "OpenAPI")
        System(XML, "XML")
        System(JS, "JSONSchema")
        System(CSV, "CSV")

      }
      Rel(NDC, JSON, "projection")
      Rel(NDC, JS, "projection")
      Rel(NDC, XML, "projection")
      Rel(NDC, OAS, "projection")
      Rel(NDC, CSV, "projection")

```

Partendo dal vocabolario Countries possiamo utilizzare la specifica JSON-LD Framing
per estrarre un sottoinsieme dei dati in formato CSV o JSON, oppure creare un'API
che presenti i dati del vocabolario sotto forma di uno schema dati, eventualmente filtrati.

```yaml
# Stati che iniziano per `S`
SchemaVocabulary:
  x-count: 2
  x-version: 20210929-0
  anyOf:
    - enum:
        - USA
      externalDocs:
        url: http://publications.europa.eu/resource/authority/country/USA
      title: Stati Uniti
      type: string
    - enum:
        - VAT
      externalDocs:
        url: http://publications.europa.eu/resource/authority/country/VAT
      title: Stato della Città del Vaticano
      type: string
```

## Semantica e sintassi

Uno dei problemi principali da affrontare è quello della dicotomia tra semantica e sintassi.

Gli erogatori di API di solito specificano informazioni semantiche in documenti di testo non machine-readable
e vedono semantiche e sintassi condivise come un vincolo ulteriore alla creazione di servizi digitali,
oppure percepiscono il complesso delle tecnologie semantiche come un'inutile complessità;
nella migliore delle ipotesi, queste informazioni sono descritte in prosa, come nell'esempio seguente:

```yaml
Person:
  description: A Person.
  type: object
  properties:
    givenName:
      description: The given name of a Person.
      type: string
    familyName:
      description: The family name, or surname, of a Person.
      type: string
  example:
    givenName: John
    familyName: Doe

```

Un approccio completamente semantico (ad es. API in formato RDF) non si è diffuso per l'overhead computazionale legato al trasferimento e al processamento in ogni messaggio
delle informazioni semantiche.
Inoltre, il panorama semantico non fornisce modi semplici per definire/limitare la sintassi di un oggetto: strumenti come [shacl](https://www.w3.org/TR/shacl/) e [owl restrictions](https://www.w3.org/TR/owl2-overview/) sono considerati computazionalmente intensivi e complessi da utilizzare dagli sviluppatori web e mobile.
La scelta più semplice resta quindi quella di utilizzare specifiche del mondo RDF per la semantica dei dati,
e specifiche del mondo REST/SOAP per definire la sintassi.

Il documento [REST API Linked Data Keywords](https://datatracker.ietf.org/doc/draft-polli-restapi-ld-keywords/) definisce un meccanismo semplice
per integrare in un JSON Schema dei riferimenti semantici utilizzando delle keyword specifiche che non confliggono con altri standard.

```yaml
Person:
  "x-jsonld-type": "https://schema.org/Person"
  "x-jsonld-context":
     "@vocab": "https://schema.org/"
     country:
       "@id": addressCountry
       "@language": en
  type: object
  required:
  - given_name
  - family_name
  properties:
    familyName: { type: string, maxLength: 255  }
    givenName:  { type: string, maxLength: 255  }
    country:    { type: string, maxLength: 3, minLength: 3 }
    custom_id:  { type: string, maxLength: 255  }
  example:
    familyName: "Doe"
    givenName: "John"
    country: "FRA"
```
