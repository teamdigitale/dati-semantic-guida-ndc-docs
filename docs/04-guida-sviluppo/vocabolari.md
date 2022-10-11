## Vocabolari controllati

I vocabolari controllati pubblicati DEVONO essere conformi
alle relative Linee guida nazionali.

I vocabolari controllati DEVONO essere pubblicati solo in formato RDF/Turtle (media type `text/turtle`)
e l’estensione del file DEVE essere `.ttl`.

### Proiezione in formato CSV

Le directory del vocabolario controllato DOVREBBERO contenere una proiezione in formato CSV del vocabolario
insieme ai metadati necessari per mappare i campi del CSV alle risorse presenti nell’RDF.
L’estensione del file DEVE essere .csv.

I metadati del CSV DOVREBBERO essere pubblicati in un frictionless data package,
posizionato nella stessa directory ed
annotato con tramite le specifiche indicate in REST API Linked Data Keywords.

La proiezione CSV deve rispettare i seguenti requisiti:

1. è possibile inserire dei commenti, che iniziano con il carattere `#`;
1. la prima riga utile DEVE contenere i nomi delle colonne;
1. le righe seguenti DEVONO contenere i valori delle risorse separati da `,` (virgola)
   e racchiusi in `"` (doppie virgolette);
1. la proiezione DOVREBBE essere generata utilizzando strumenti quali JSON-LD framing.

Questa proiezione in formato CSV viene esposta dalla NDC tramite API REST.

I metadati di cui sopra DEVONO essere espressi tramite un `@context` JSON-LD 1.1.

(vocabolari-esempi)=
### Esempi

Di seguito l’esempio di un’alberatura contenente
un vocabolario controllato e la sua proiezione in formato CSV
generata utilizzando le informazioni di framing indicate in
`framing.yamlld`.
Il file `datapackage.yaml` contiene i metadati del CSV.

```bash
assets/
  controlled-vocabulary/
    my-codelist/
      CHANGELOG.md
      README.md
      my-codelist.ttl
      my-codelist.csv
      datapackage.yaml
      framing.yamlld
```

Il file my-codelist.ttl contiene il vocabolario controllato in formato RDF/Turtle.

```turtle
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
```

The file my-codelist.csv contains the projection of the controlled vocabulary in CSV format.

```csv
# It is possible to add comments
#   metadata is into datapackage.yaml
"id","label_en","label_it","label_fr"
"ITA","Italy","Italia","Italie"
"DEU","Germany","Germania","Allemagne"
"ESP","Spain","Spagna","Espagne"
```

Datapackage contains all metadata information about the CSV file.

```yaml
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
```

(vocabolari-versionamento)=
### Versionamento

La versione attuale di NDC pubblica solamente l’ultima versione dei vocabolari controllati.
L’Erogatore è responsabile della pubblicazione delle versioni precedenti dei vocabolari
tramite il repository git.

I vocabolari che pubblicano informazioni soggette a variazioni nel tempo,
DOVREBBERO versionare i singoli record.
Si veda a questo proposito il vocabolario controllato dei Paesi pubblicato
dall’Unione Europea: https://publication.europa.eu/resource/authority/country/
dove i singoli record contengono l’intervallo di validità dei dati.
