## Vocabolari controllati

I vocabolari controllati pubblicati DEVONO essere conformi
alle relative Linee guida nazionali.

I vocabolari controllati DEVONO essere pubblicati solo in formato RDF/Turtle (media type `text/turtle`)
e l’estensione del file DEVE essere `.ttl`.

Le directory del vocabolario controllato DOVREBBERO contenere una proiezioni in formato CSV del vocabolario
insieme ai metadati necessari per mappare i campi del CSV alle risorse presenti nell’RDF.
Questa proiezione in formato CSV viene esposta dalla NDC tramite API REST.
L’estensione del file DEVE essere .csv.

I metadati di cui sopra DEVONO essere espressi tramite un `@context` JSON-LD 1.1.

(vocabolari-esempi)=
### Esempi

Di seguito l’esempio di un’alberatura contenente
un vocabolario controllato e la sua proiezione in formato CSV.

```bash
assets/
  controlled-vocabulary/
    my-codelist/
      CHANGELOG.md
      README.md
      my-codelist.ttl
      my-codelist.csv
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
