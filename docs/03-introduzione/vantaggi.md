## Vantaggi

NDC semplifica la creazione di servizi digitali.

Aiuta i progettisti e gli sviluppatori di servizi a:

- utilizzare concetti appropriati;
- riusare gli schemi e i vocabolari controllati (codelist, tassonomie).
-
Supporta le agenzie:

- nell'indicizzazione e nella pubblicazione di risorse semantiche;
- nella cooperazione nella progettazione di asset semantici.

E' inoltre basato su standard riconosciuti (RDF, JSON-LD) e altri in via di consolidamento (YAML, YAML-LD, REST API Linked Data Keywords).

Di seguito alcuni esempi che illustrano i vantaggi di NDC

### Sviluppo cooperativo di ontologie

Sviluppare cooperativamente ontologie ed asset semantici in genere, è un processo complesso.
Un catalogo centralizzato permette di creare degli indicatori quantitativi
basati sul numero di asset prodotti, e di misurare quindi i progressi in termini di interoperabilità semantica e sintattica.

Sebbene richieda uno sforzo, avere asset semantici condivisi riduce i costi di creazione
dei nuovi servizi, e quelli di integrazione con altri servizi.
Ogni variazione agli schemi dati e alla semantica infatti richiede delle conversioni,
che vanno testate scrivendo codice di test sia per la parte semantica che sintattica.
Il volume (ed il costo) di questo codice - che va manutenuto nel tempo - aumenta con il numero di servizi che devono essere integrati.

```{mermaid}

flowchart LR
    classDef default stroke:white,color:#fff,clusterBkg:none,fill:#3344d0
    classDef cluster font-weight: bold,fill:none,color:darkgray,stroke:#3344d0,stroke-width:2px
    classDef subgraph_padding fill:none, stroke:none, opacity:0
    classDef bounded_context stroke-dasharray:5 5

subgraph Converters increase costs
subgraph p1
direction LR
Agency1
Agency2
Agency3
end
end

class p1 subgraph_padding

subgraph Agency1
schema1[/schema 1/]
service1
convert(convert to 2)
convert13(convert to 3)
end

subgraph Agency2
service2
schema2[/schema 2/]
end

subgraph Agency3
service3
schema3[/schema 3/]
end

service1 --> convert --> service2
service1 --> convert13 --> service3
schema1  -.- service1
service2 -.-o schema2
service3 -.-o schema3

```

Lo sviluppo di asset semantici quindi è un investimento che ripaga nel tempo.


### Riuso di asset semantici

Il riuso di asset semantici è un altro vantaggio di NDC. I service designer non dovranno modellare in continuazione concetti esistenti, ma potranno ricercarli sul catalogo.

```{mermaid}

flowchart LR
    classDef default stroke:white,color:#fff,clusterBkg:none,fill:#3344d0
    classDef cluster font-weight: bold,fill:none,color:darkgray,stroke:#3344d0,stroke-width:2px
    classDef subgraph_padding fill:none, stroke:none, opacity:0
    classDef bounded_context stroke-dasharray:5 5


    subgraph Dev[fa:fa-user Service Developer ]
    direction LR
    0start((design\nservice)) -->
    1_lookup[Search\nNDC for\nassets] -->
    2_reuse[reuse\nschemas] -->
    3_design[design\nAPI] -->
    4_validate[validate\nAPI design] -->
    5_create_bundle[sign semantic\nbundle ] -->
    E((end))
    end
    5_create_bundle -->
    6_upload_pdnd[upload to \n pdnd]
```

I visualizzatori presenti (e quelli che verranno aggiunti in futuro) permettono di navigare i vari concetti in modo che sia semplice individuare i sottoinsiemi di dati che possono essere riutilizzati.

La modellazione dei dati relativi al titolo di studio ad esempio, potrà riusare il concetto e le classificazioni presenti in [EducationLevel](https://w3id.org/italia/onto/CPV/EducationLevel).

### Vocabolari controllati come schemi dati

I vocabolari controllati sono un altro tipo di asset semantici pubblicati in formato RDF su NDC.
Il vocabolario con l'elenco dei comuni può essere utilizzato per modellare i dati relativi alla residenza di una persona;
mentre il vocabolario dei titoli di studio per modellare un form relativo al grado di istruzione.

```{mermaid}

flowchart LR
    classDef default stroke:white,color:#fff,clusterBkg:none,fill:#3344d0
    classDef cluster font-weight: bold,fill:none,color:darkgray,stroke:#3344d0,stroke-width:2px
    classDef subgraph_padding fill:none, stroke:none, opacity:0
    classDef bounded_context stroke-dasharray:5 5

subgraph Users
Agency1
Agency2
end

subgraph Agency1
WebForm[Web Form]
end

subgraph Agency2
API[API Specification]
end

WebForm & API --> |reuse schema| el_jsonschema

subgraph schema.gov.it
subgraph schema.gov.it_p
EducationLevel
end
end

subgraph EducationLevel
subgraph EducationLevel_p
el_rdf[/RDF/]
el_jsonschema[/JSON Schema/]
end
end

class EducationLevel_p,schema.gov.it_p subgraph_padding
class Users subgraph_padding
```

Per permettere questo tipo di riuso, è necessario pubblicare i vocabolari controllati non solo in formato RDF, ma anche in un formato che indichi la proiezione specifica da utilizzare per generare il JSON Schema: questo formato è basato sulle specifiche Frictionless Data.
