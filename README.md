# Progetto IDS: Analisi della Correlazione Qualifica-Gara in Formula 1 e Impatto della Tipologia di Circuito

**Autori:** Nicolò Calandra, Andrea Di Blasi

## 1. Introduzione

Questo progetto si addentra nell'analisi dei dati storici della Formula 1 (dal 1950 al 2024) con l'obiettivo principale di studiare la **correlazione tra la posizione ottenuta dai piloti in qualifica e il loro piazzamento finale in gara**. Un focus cruciale dell'analisi è determinare come questa correlazione sia modulata dalla **tipologia del circuito**.

Attraverso l'esplorazione dei dati, test statistici e lo sviluppo di un modello di regressione logistica, cerchiamo di comprendere se e come le caratteristiche intrinseche di un tracciato (classificato come Tecnico, ad Alta Velocità o Misto) influenzino l'importanza strategica della posizione di partenza sul risultato della competizione.

## 2. Tipologie di Circuito Definite

Per condurre un'analisi mirata, i circuiti di Formula 1 sono stati classificati in tre categorie principali, basate sulle loro caratteristiche predominanti:

1.  **Circuito Tecnico:** Caratterizzato da un elevato numero di curve e sezioni a bassa velocità, dove l'abilità di guida del pilota e l'agilità della vettura sono fattori determinanti.
    *   *Esempi (ipotetici per il progetto): Monaco, Hungaroring.*
2.  **Circuito ad Alta Velocità:** Tracciati con lunghi rettilinei e poche curve impegnative, dove la potenza del motore e l'efficienza aerodinamica giocano un ruolo preponderante.
    *   *Esempi (ipotetici per il progetto): Monza, Spa-Francorchamps (in parte).*
3.  **Circuito Misto:** Circuiti che offrono una combinazione bilanciata di sezioni tecniche guidate e tratti ad alta velocità, richiedendo un compromesso nell'assetto della vettura e una versatilità da parte del pilota.
    *   *Esempi (ipotetici per il progetto): Silverstone, Barcellona.*

*(La classificazione specifica usata nel progetto è documentata nel file `f1db-circuits.csv` arricchito).*

## 3. Dataset Utilizzato

L'analisi si fonda sul dataset **F1DB**, una raccolta completa di informazioni storiche sulla Formula 1. I dati grezzi in formato CSV, utilizzati per questo studio, sono localizzati nella cartella `f1db-csv/` e includono:

*   `f1db-circuits.csv`: Informazioni dettagliate sui circuiti. **Questo file è stato da noi arricchito** con una colonna `track_type` contenente la classificazione del circuito (Tecnico, Alta Velocità, Misto) secondo le definizioni sopra.
*   `f1db-races.csv`: Dettagli generali su ogni singola gara disputata.
*   `f1db-races-race-results.csv`: Risultati finali delle gare per ogni pilota, incluse posizioni di partenza e di arrivo.
*   `f1db-races-driver-standings.csv`: Classifica generale dei piloti aggiornata prima di ogni gara, utilizzata per derivare una feature rappresentativa della "forma" o performance storica del pilota.

## 4. Struttura del Progetto

```
Formula-1-analysis/
├── f1db-csv/                 # Cartella contenente i file CSV del dataset
│   ├── f1db-circuits.csv
│   ├── f1db-races.csv
│   ├── f1db-races-race-results.csv
│   └── f1db-races-driver-standings.csv
├── README.md                 # Questo file
└── progetto.ipynb            # Jupyter Notebook con l'analisi completa
└── gara04-05-25.csv          # File CSV per testare il modello (esempio)
└── test-tecnico.csv          # File CSV per testare il modello su circuiti tecnici (esempio)
└── test-alta-velocita.csv    # File CSV per testare il modello su circuiti veloci (esempio)
└── test-misto.csv            # File CSV per testare il modello su circuiti misti (esempio)
```

## 5. Requisiti e Installazione

Per eseguire l'analisi contenuta nel notebook `progetto.ipynb`, è necessario avere Python 3.x e le seguenti librerie installate:

*   `pandas` (per la manipolazione dei dati)
*   `numpy` (per calcoli numerici)
*   `matplotlib` (per la creazione di grafici)
*   `seaborn` (per visualizzazioni statistiche avanzate)
*   `scipy` (per test statistici)
*   `scikit-learn` (per il modello di machine learning)
*   `jupyter` (per eseguire il notebook)

Puoi installare tutte le dipendenze necessarie utilizzando `pip` e il file (da creare) `requirements.txt`:

```bash
pip install -r requirements.txt
```
Oppure, singolarmente:
```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn jupyter
```

## 6. Come Eseguire l'Analisi

1.  **Clonare il Repository (se applicabile):**
    ```bash
    # Esempio: git clone https://github.com/tuo-username/Formula-1-analysis.git
    # cd Formula-1-analysis
    ```
2.  **Verificare il Dataset:** Assicurati che la cartella `f1db-csv/` con i relativi file CSV sia presente nella directory principale del progetto.
3.  **Installare le Dipendenze:** Segui le istruzioni nella sezione "Requisiti e Installazione".
4.  **Avviare Jupyter:** Apri ed esegui il notebook `progetto.ipynb` tramite Jupyter Notebook o Jupyter Lab:
    ```bash
    jupyter notebook progetto.ipynb
    ```
    o
    ```bash
    jupyter lab progetto.ipynb
    ```
    Esegui le celle del notebook in sequenza.

## 7. Sommario dell'Analisi e Risultati Chiave

Il notebook `progetto.ipynb` documenta l'intero processo analitico, dalla preparazione dei dati alla modellazione. Di seguito, un riepilogo dei passaggi principali e dei risultati emersi.

### 7.1. Preparazione e Pulizia dei Dati
*   Caricamento dei diversi CSV e fusione in un dataframe analitico principale (`df`).
*   Gestione dei valori mancanti e conversione dei tipi di dati.
*   Creazione di feature aggiuntive, come `podio` (variabile target binaria) e `classifica_pre_gara_rank`.
*   Filtraggio dei dati per includere solo le gare a partire dall'anno 2000, per focalizzarsi su ere più moderne e consistenti della F1.

### 7.2. Analisi Esplorativa dei Dati (EDA)

L'EDA si è concentrata sulla comprensione delle distribuzioni e delle relazioni tra le variabili chiave, segmentate per tipo di circuito.

*   **Distribuzione delle Posizioni Finali:**
    *   Sono stati generati istogrammi e box plot per visualizzare la distribuzione delle posizioni finali dei piloti.
    *   **[Placeholder per Grafico: Istogramma/Box Plot delle Posizioni Finali per Tipo di Circuito]**
        *   *Commento*: Questi grafici hanno rivelato che [breve descrizione di cosa si osserva, es. i circuiti Tecnici mostrano una mediana di posizione finale leggermente migliore per i piloti partiti davanti, o una minore dispersione dei risultati].
*   **Confronto Media vs. Mediana della Posizione Finale:**
    *   L'analisi della differenza tra media e mediana della posizione finale ha indicato la presenza di asimmetria e potenziali outlier, con differenze più marcate per circuiti ad Alta Velocità e Misti, suggerendo una maggiore dispersione verso posizioni di arrivo più alte (peggiori) in questi contesti.
    *   **[Placeholder per Tabella/Grafico: Confronto Media-Mediana Posizione Finale per Tipo Circuito]**
*   **Analisi "OLAP Style" - Arrivi sul Podio:**
    *   È stata esaminata la percentuale di arrivi sul podio in base alla posizione di partenza e al tipo di circuito.
    *   **[Placeholder per Grafico: Percentuale Podi vs. Posizione di Partenza per Tipo Circuito]**
        *   *Commento*: Questa analisi ha evidenziato come, ad esempio, sui circuiti Tecnici, partire nelle primissime file sembri offrire un vantaggio più marcato per l'accesso al podio rispetto ai circuiti di Alta Velocità.

### 7.3. Test Statistici
*   Sono stati eseguiti test t (o test non parametrici equivalenti, se le assunzioni non fossero rispettate) per confrontare statisticamente le medie delle posizioni finali tra diverse posizioni di partenza (es. P1 vs P2, P2 vs P3) all'interno di ciascuna categoria di circuito.
*   *Risultato Chiave*: Questi test hanno generalmente confermato che partire più avanti è associato a una posizione finale media significativamente migliore. L'entità di questa differenza, tuttavia, mostra variazioni a seconda del tipo di circuito.

### 7.4. Modello di Regressione Logistica

È stato sviluppato un modello di regressione logistica per predire la probabilità che un pilota termini la gara **sul podio** (`podio = 1`).

*   **Features Selezionate:**
    *   `posizione_partenza` (numerica)
    *   `classifica_pre_gara_rank` (numerica, usata come proxy per la "forma" e l'abilità storica del pilota)
    *   Tipo di circuito (categorica, gestita tramite one-hot encoding: `circuito_Tecnico`, `circuito_Alta_velocita`, `circuito_Misto`).
*   **Variabile Target:** `podio` (binaria: 1 se il pilota è arrivato tra i primi tre, 0 altrimenti).
*   **Valutazione del Modello:**
    *   Il dataset è stato suddiviso in training set e test set.
    *   Le performance del modello sono state valutate utilizzando metriche appropriate per la classificazione:
        *   **Accuracy:** [Valore, es. 0.XX] (confrontata con l'accuracy di un modello nullo).
        *   **Matrice di Confusione:**
            ```
            [[TN  FP]
             [FN  TP]]
            ```
            **[Placeholder per Immagine: Matrice di Confusione del Modello]**
        *   **Precisione (Precision):** [Valore, es. 0.XX]
        *   **Richiamo (Recall):** [Valore, es. 0.XX]
        *   **F1-Score:** [Valore, es. 0.XX]
        *   **Curva ROC e AUC (Area Under Curve):** [Valore AUC, es. 0.XX]
            **[Placeholder per Grafico: Curva ROC del Modello]**
    *   *Commento*: Il modello ha dimostrato [breve descrizione della performance, es. una buona capacità predittiva, superando il modello nullo, con un AUC di...].
*   **Interpretazione dei Coefficienti:** L'analisi dei coefficienti del modello ha fornito insight sull'impatto (positivo o negativo) e sulla significatività di ciascuna feature sulla probabilità (log-odds) di ottenere un podio.
*   **Test su Nuovi Dati:** Il modello addestrato è stato utilizzato per effettuare predizioni su set di dati di test appositamente creati (`test-tecnico.csv`, `test-alta-velocita.csv`, `test-misto.csv`), simulando scenari di gara reali e valutando la coerenza delle previsioni con le aspettative qualitative.

## 8. Conclusioni Principali

L'analisi condotta e i risultati del modello di regressione logistica suggeriscono che:

1.  La **posizione di partenza è un fattore statisticamente significativo** e cruciale nel determinare la posizione finale e la probabilità di raggiungere il podio in Formula 1.
2.  L'**importanza relativa della posizione di partenza varia in modo apprezzabile con la tipologia di circuito**: sui tracciati tecnici, un'ottima qualifica sembra tradursi in un vantaggio più consolidato rispetto ai circuiti ad alta velocità, dove altri fattori possono rimescolare maggiormente le carte.
3.  La **performance storica e la "forma" del pilota** (approssimata dalla sua classifica pre-gara) costituiscono un altro predittore rilevante per il successo in gara.
4.  Il modello di regressione logistica, sebbene semplice, si è dimostrato capace di catturare queste dinamiche e fornire **previsioni utili**, fungendo da solida baseline per eventuali modelli più complessi.

## 9. Possibili Sviluppi Futuri

*   **Ingegnerizzazione di Nuove Feature:** Esplorare l'aggiunta di variabili come le condizioni meteorologiche, l'affidabilità specifica del team/motore in quella stagione, l'esperienza del pilota sul circuito specifico.
*   **Modelli Alternativi:** Testare algoritmi di machine learning più avanzati (es. Random Forest, Gradient Boosting, Reti Neurali) per valutare se possono offrire un incremento di performance predittiva.
*   **Analisi Temporale più Granulare:** Studiare come le correlazioni siano cambiate attraverso ere regolamentari diverse all'interno del periodo post-2000.
*   **Analisi di Segmenti Specifici:** Approfondire l'analisi per specifiche fasce di piloti (es. top team vs. midfield) o per specifiche posizioni di arrivo oltre il podio.
*   **Deployment Semplificato:** Creare una piccola applicazione web (es. con Streamlit o Flask) per interagire con il modello e fare previsioni su ipotetiche gare.

---

*(Questo README è un documento vivo e può essere ulteriormente dettagliato con grafici specifici e metriche precise direttamente dal notebook `progetto.ipynb` una volta finalizzata ogni sua parte).*
