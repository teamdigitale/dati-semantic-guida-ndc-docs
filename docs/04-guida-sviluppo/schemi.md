## Schemi OpenAPI

Gli schemi pubblicati devono essere conformi alle relative Linee guida nazionali.

Gli schemi per le API devono essere pubblicati in formato OpenAPI3 (corrispondenti ad una estensione di [JSON Schema Draft 4](https://spec.openapis.org/oas/v3.0.3#data-types)), incorporato nella sezione `#/components/schema` del file OAS
compatibilmente con le Linee Guida per l'interoperabilità tecnica.
L’estensione del file DEVE essere `.oas3.yaml`.

In futuro potranno essere supportati altri formati di schemi (e.g. versioni più recenti di JSON Schema).

Il file YAML DOVREBBE contenere i riferimenti semantici descritti nel documento [I-D-polli-restapi-ld-keywords](https://datatracker.ietf.org/doc/draft-polli-restapi-ld-keywords/)
attraverso:

- il campo custom `x-jsonld-context` contenente un `@context` JSON-LD conforme alle indicazioni contenute in JSON-LD 1.1;
- il campo custom `x-jsonld-type` contenente il riferimento ad un `rdf:type`.

I metadati associati DEVONO essere pubblicati solo in formato RDF/Turtle (media type `text/turtle`)
e l’estensione del file DEVE essere `.ttl`.
Questo file DOVREBBE essere generato automaticamente dal documento OpenAPI.

Gli schemi forniti POSSONO essere verificati sintatticamente utilizzando l’[OpenAPI Checker](https://github.com/italia/api-oas-checker).

### Schema bundling

Quando si pubblica un documento OAS contenente la specifica di un’API,
è utile dereferenziare ed accorpare in un unico file tutti i riferimenti
a schemi ed operazioni.
Questo processo viene detto [bundling](https://json-schema.org/understanding-json-schema/structuring.html#bundling).
Il prodotto sarà un singolo OAS document (e.g. un file YAML) utile alla validazione sintattica e semantica
dell’API.
Questo meccanismo permette di inserire nell’IDL tutte le informazioni semantiche necessarie
a descrivere l’API in base sia ai riferimenti ontologici che agli schemi utilizzati.

### Esempi

Un esempio di file OAS3 metadatato con i campi `x-jsonld-context` e `x-jsonld-type`:

```yaml
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
```


Di seguito l’esempio di un’alberatura contenente uno schema

```bash
assets/
  schemas/
    Person/
      CHANGELOG.md
      README.md
      person.oas3.yaml
      person.index.ttl
```


## Schemi XSD

Attualmente il materiale semantico pubblicato dalla UE si basa sui formati RDF ed XSD.
NDC non supporta il processamento di file XSD.
Questi potranno essere supportati in un secondo momento.

### Esempio: Countries Authority Table

L'authority table dei paesi "Countries" viene pubblicata a partire dall'URL su http://publications.europa.eu/resource/dataset/country contenente i link a tutti i dataset associati e corrispondente al suo URI.
All'indirizzo https://publications.europa.eu/resource/authority/country si trova l'elenco dei paesi in formato RDF; sotto quell'URL ci sono i riferimenti ai singoli paesi, eg. https://publications.europa.eu/resource/authority/country/ITA.
Il versionamento è contenuto all'interno degli RDF e l'URL viene dereferenziato all'ultima versione.
Gli URI sono versionati, eg. http://publications.europa.eu/resource/expression/country/20170920-0
Da lì è possibile individuare una lista di dataset associati ed eventualmente localizzati:
qui https://publications.europa.eu/resource/cellar/07ed8d46-2b56-11e7-9412-01aa75ed71a1.0001.12/DOC_14 la lista delle coppie codice/paese in italiano in formato XML (ATTO table, usate per le traduzioni)

```xml
<TABLE VL="IT" NAME="countries">
  <LIBELLE CODE="1A0">Kosovo</LIBELLE>
  <LIBELLE CODE="ABW">Aruba</LIBELLE>
  <LIBELLE CODE="AFG">Afghanistan</LIBELLE>
...
</TABLE>
```

qui una codelist (estensione ".gc") http://publications.europa.eu/resource/distribution/country/20210616-0/xml/gc/Country.gc contenente tutti i dati in un formato xml analogo a quello tabellare

```xml
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
```

Gli stessi dati possono essere recuperati  a partire da https://data.europa.eu/data/datasets/country.



### Versionamento

TBD
