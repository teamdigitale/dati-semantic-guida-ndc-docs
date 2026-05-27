Indicazioni su aggiornamento di asset semantici esistenti
=========================================================

Di seguito sono riportate le raccomandazioni in presenza di proposte, 
da parte degli utenti, che richiedono modifiche ad asset semantici già esistenti.
Invece, per la modifica delle proprie risorse da parte dei titolari delle stesse,
si rinvia al `paragrafo "Contribuzione continua al catalogo" <../come-contribuire/contribuzione-continua-al-catalogo.html>`__

Modifiche a vocabolari controllati esistenti
--------------------------------------------

Qualora si propongano modifiche a vocabolari esistenti è necessario
specificare nella proposta quanto segue:

-  se un concetto già esistente è da considerarsi deprecato. Nel qual
   caso si dovrà aggiungere al concetto la proprietà ``owl:deprecated`` per
   indicare che non è più valido;

-  aggiungere la definizione del/dei nuovo/nuovi concetto/i seguendo
   esattamente le definizioni dei concetti già esistenti nel vocabolario
   (anche in termini di URI);

-  qualora si voglia aggiungere un nuovo livello a una tassonomia o a un
   tesauro, è necessario motivare la richiesta e predisporre il nuovo
   livello considerando l’aggiunta delle proprietà ``skos:narrower`` e
   ``skos:broader`` prima menzionate ove applicabili nei livelli precedenti già
   presenti nel vocabolario controllato.

Modifiche a ontologie esistenti
-------------------------------

Le modifiche vengono esplicitate evidenziando i requisiti (domande di
competenza) che portano a richiedere la modifica di concetti e/o
proprietà già esistenti o cambiamenti nelle restrizioni *OWL* attualmente
inserite nelle ontologie esistenti. Le domande di competenza sono di
fatto interrogazioni sui dati che la modellazione deve poter supportare.

Nuovi concetti e/o proprietà rispetto a quelle esistenti, sempre
motivate da specifici requisiti da evidenziare, dovranno essere definiti
seguendo esattamente le definizioni già fornite nell’ambito delle
ontologie esistenti (i.e., specificando tutte le annotazioni che già
vengono utilizzate sia in lingua italiana che in lingua inglese,
specificando eventuali restrizioni *OWL* se necessarie).

Si raccomanda di non effettuare cambiamenti negli URI per concetti e/o
proprietà già definite, per via della loro natura di identificativi
univoci e soprattutto persistenti nel tempo, eccetto il caso in cui i
cambiamenti siano indispensabili per garantire un funzionamento
complessivo dell’asset (anche in termini di coerenza semantica) e del
Catalogo, o quando gli URI contengono evidenti errori di
battitura che ne possano compromettere l'usabilità e la leggibilità.

Modifiche a schemi dati 
------------------------

Le modifiche da proporre a schemi dati saranno valutate nel caso in cui
saranno evidenziati nuovi casi d’uso. Sulla base di queste nuove
necessità si decide se modificare uno schema dati già esistente o
crearne uno nuovo. Le modifiche proposte per gli schemi dati dovranno
seguire tutte le regole sintattiche e semantiche definite nel contesto
del Catalogo.
