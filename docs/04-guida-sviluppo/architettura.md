(architettura)=
# Architettura di schema.gov.it

L'architettura di schema.gov.it è descritta dal seguente diagramma:

1. gli enti popolano i loro repository semantici
   conformemente alle indicazioni tecniche contenute in questo documento e registrano i loro repository
   nel Catalogo del Riuso disponibile su <https://developers.gov.it/it/software>;
1. NDC recupera l'elenco dei repository dal Catalogo Software e li processa, popolando i datastore interni della piattaforma;
1. gli utenti possono ricercare ed accedere ai dati sia con interfacce utente (sito web e visualizzatori semantici) che tramite diverse tipologie di API (REST, SparQL, ...)

```{mermaid}
   flowchart BT
      classDef default stroke:white,color:#fff,clusterBkg:none,fill:#3344d0
      classDef cluster font-weight: bold,fill:none,color:darkgray,stroke:#3344d0,stroke-width:2px
      classDef subgraph_padding fill:none, stroke:none, opacity:0
      classDef bounded_context stroke-dasharray:5 5

      subgraph Repositories
      subgraph pad
         Ontopia
         Altri
      end
      end
      subgraph Altri
         Ente1
         Ente2
         Ente2 --- Ente1
         linkStyle 0 stroke:none
      end

      subgraph sgi[schema.gov.it]
      subgraph p1
        direction TB
        DB
        APIL
        UI
        x
        %% formatting
        DB -.- APIL & UI
        linkStyle 1,2 stroke:none
      end
      end



      subgraph APIL [API]
      subgraph APILp [ ]
            direction TB
              SparQLAPI[SparQL API] & API[REST] & API2[Schema API]
      end
      end

      subgraph UI [User Interface]
      subgraph UIp
        direction BT

        WebUI
        SemanticViewers
      end
      end

      subgraph DB[Data]
      direction TB
        Index[(Index DB)]
        SparQL[(Graph DB)]
        Other[(Other DBs...)]
      end
        subgraph x [ ]
        P[[Harvesters]]
        end
        P --->|write| DB

      Ontopia -->|harvesting| P
      Altri -->|harvesting| P
      APIL -.-o|read| DB
      UI -.-o|read| DB
      subgraph Ontopia["Ontopia"]
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
      class Altri,Repositories bounded_context
      class pad,p1,UIp,APILp,x subgraph_padding
   ```
