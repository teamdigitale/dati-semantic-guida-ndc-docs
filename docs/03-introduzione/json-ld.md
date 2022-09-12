### Specificare la semantica tramite JSON LD

JSON LD descrive una serializzazione di RDF basata su JSON.

Ad esempio, usando la mappatura definita in https://schema.org/docs/jsonldcontext.jsonld,
è possibile interpretare questo oggetto JSON come un RDF.

```json
{
  "@context": "http://schema.org/",
  "@type": "Person",
  "name": "Jane Doe",
  "jobTitle": "Professor",
  "telephone": "(425) 123-4567"
}
```

È anche possibile ridefinire o localizzare i campi come di seguito, eventualmente usando diversi namespace.

```
"@context":
  "sdo": "http://schema.org/"
  "nome":"sdo:name"
  "nome_proprio": "sdo:givenName"
"@type": "Person"
"nome": "Jane Doe"
"nome_proprio": "Jane"
"sdo:jobTitle": "Professor"
"sdo:telephone": "(425) 123-4567"
```

Poiché un oggetto definito esclusivamente tramite json-ld porta con sé la propria definizione,
per validarlo occorre innanzitutto risolvere le referenze, quindi verificarle.
Questo si presta bene ad un processamento batch,
ma è complesso da usare in un contesto sincrono:
anche perché fino al momento del processamento del `@context`
non c'è nessuna garanzia della correttezza dei campi da processare.

Nella creazione di un'API di solito gli schemi utilizzati sono consolidati in fase di specifica, quindi i dati indicati in @context e @type sono desunti dall'operazione. Può essere utile in alcuni casi ritornare il contesto semantico di un oggetto solo quando il client lo richiede (eg. `Accept: application/ld+json` o tramite un HTTP header `Link`): anche in questo caso è utile definirlo chiaramente a priori e stabilire un modello che minimizzi:

- la dimensione del payload;
- le operazioni di verifica, considerando sempre che in ogni processo in cui il mittente può guidare il meccanismo di verifica (ad esempio indicando il parser per deserializzare una stringa) si possono configurare dei problemi di sicurezza come nei seguenti casi:

```python
yaml.load("!!python/object/new:os.system [echo BOOM!]")
```

- https://www.ws-attacks.org/Soap_Array_Attack
- "@context" duplicato in json-ld, dove la specifica indica che l'ultimo valore è sovrascrive il primo, vedi https://w3c.github.io/json-ld-bp/#example-12-overriding-name-term;
- "@context" mangling, dove cambiando il "@context" di una risposta eventualmente firmata si riesce a modificare la semantica di un oggetto senza modificarne la forma (eg, https://github.com/json-ld/json-ld.org/issues/213);

Nel caso di informazioni localizzate, JSON-LD permette di trasmettere l'informazione in diversi modi semanticamente equivalenti, eg.

```
-- come lista
occupation:
-  @value: "Student"
   @language: en
-  @value: "Etudiant"
   @language: fr
```

o

```
-- come oggetto
@context:
  occupation:
    @container: @language
occupation:
  en: Student
  fr: Etudiant
```

Il @context può essere espresso più brevemente impostando un vocabolario di base tramite @vocab:

```
"@context":
  "@vocab":   "https://w3id.org/italia/onto/CPV/"
  given_name:  givenName
  family_name: familyName
```

Quello più simile al modello di content-negotiation usato comunemente con `Accept-Language` (dove basta rimuovere il "@context" è questo

```
--- tramite elementi multipli, utile anche per la serializzazione di API semplici
@context:
  occupation: {@language: en}
  occupation_fr: {@language: fr}
occupation: Student
occupation_fr: Etudiant
```

Oltre che indicare una serializzazione basata su JSON di RDF, permette di interpretare un JSON object
come RDF specificando una mappatura tra le chiavi dell'oggetto ed i predicati dell'RDF.

È possibile ad esempio collegare dinamicamente un oggetto in formato json-schema col suo @context attraverso un HTTP Header Link. Ad esempio, una response contenente un JSON conforme al seguente json-schema

```
Person:
  type: object
  required: [given_name, family_name]
  properties:
    given_name: {type: string}
    family_name: {type: string}
    pippo: {type: string}
```

può essere collegata al @context di seguito usando le indicazioni contenute in https://www.w3.org/TR/json-ld11/#interpreting-json-as-json-ld

Di seguito un esempio di richiesta e di risposta.

```
GET /user/1234
Host: example.com
Accept: application/json
```

Risposta:

```
HTTP/1.1 200 OK
Content-Type: application/json
Link: <https://schemas.ndc.gov.it/italia/simple-person.jsonld>;
     rel="http://www.w3.org/ns/json-ld#context"; type="application/ld+json"

{ "given_name": "Roberto", "family_name": "Polli" }
```
