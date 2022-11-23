## Ontologie

Le ontologie pubblicate DEVONO essere conformi alle relative Linee guida nazionali.

Le ontologie DEVONO utilizzare delle directory versionate come descritto in [versionamento].

### Esempi

Esempio di alberatura contenente i file che definiscono un’ontologia.
In questo caso viene processata solo la directory `latest/`.
Nell’esempio, l’alberatura contiene una serie di file di documentazione opzionali che non vengono processati.

```bash
assets/
  ontologies/
    MyOntology/
      CHANGELOG.md
      README.md
      v1.2/
        MyOntology.ttl
      v1.1/
        MyOntology.ttl
      latest/
        MyOntology.ttl
        LATEST.md
```

(ontologie-versionamento)=
### Versionamento
All’interno delle sotto-directory di `ontologies/`,
NDC processa solo la directory con la versione più recente, ossia:

- `latest/` se presente;
- quella maggiore secondo il seguente ordinamento:

  * tra due versioni espresse come forme numeriche (con punti), si segue l’ordinamento comunemente condiviso
    per cui i numeri a sinistra sono i più significativi
  * qualora due versioni abbiano lunghezza diversa ma una sia prefisso dell’altra,
    la più lunga viene considerata più recente;
    ad esempio v4.5 è considerata obsoleta in presenza di v4.5.2.

Un repository PUO’ contenere versioni precedenti delle ontologie
per fini storici, al di là del versionamento supportato da git.

L’harvesting delle ontologie considera che le directory che contengono ontologie possano essere versionate,
non i singoli file.
Questo vale anche per le sotto-directory.

#### Esempi

Le directory versionate possono trovarsi in ogni punto dell’alberatura
delle ontologie, discendendo verso le foglie della struttura gerarchica.

Sono esempi validi:

```bash
┌─ ontologies/
│  ├─ Onto1/
│  │  ├─ latest/
│  │  │  └─ onto1.ttl
│  │  ├─ v0.5/
│  │  │  └─ onto1.ttl
│  │  ├─ v0.6/
│  │  │  └─ onto1.ttl
│  ├─ Onto2/
│  │  ├─ 0.5/
│  │  │  └─ onto2.ttl
│  │  └─ 0.6/
│  │     └─ onto2.ttl
│  └─ ...
└─ ...
```
