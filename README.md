# Progetto IDS: Analisi Correlazione Qualifica-Gara in F1

**Autori:** Nicolò Calandra, Andrea Di Blasi

## Introduzione

Questo progetto analizza i dati storici della Formula 1 per studiare la correlazione tra la posizione ottenuta dai piloti in qualifica e la loro posizione finale in gara. L'analisi si concentra su come questa correlazione varia in base alla tipologia del circuito.

L'obiettivo è comprendere se e come le caratteristiche di un tracciato influenzino l'importanza della posizione di partenza sul risultato finale.

## Tipologie di Circuito

Per l'analisi, i circuiti sono stati classificati in tre categorie principali:

1.  **Circuito Tecnico:** Piste con molte curve dove la tecnica e l'abilità del pilota sono preponderanti rispetto alla potenza del veicolo.
2.  **Circuito ad Alta Velocità:** Tracciati con lunghi rettilinei dove la potenza del motore ha un impatto maggiore sul risultato finale.
3.  **Circuito Misto:** Circuiti che presentano una combinazione equilibrata di sezioni tecniche e tratti veloci.

## Dataset

L'analisi si basa sul dataset [F1DB](<link-al-dataset-se-disponibile-o-descrizione>), che contiene dati dettagliati sulle gare di Formula 1 dal 1950 al 2024. I file CSV utilizzati si trovano nella cartella `f1db-csv`:

*   `f1db-circuits.csv`: Informazioni sui circuiti, inclusa la classificazione per tipo (aggiunta per questo progetto).
*   `f1db-races.csv`: Dettagli sulle singole gare.
*   `f1db-races-race-results.csv`: Risultati finali delle gare per ogni pilota.

## Requisiti

Per eseguire l'analisi contenuta nel notebook `progetto.ipynb`, è necessario avere installato Python e le seguenti librerie:

*   pandas
*   matplotlib
*   numpy
*   scipy

Puoi installarle usando pip:
```bash
pip install pandas matplotlib numpy scipy jupyter
```

## Come Eseguire

1.  Clona questo repository.
2.  Assicurati che la cartella `f1db-csv` contenente i dati sia presente nella directory principale del progetto.
3.  Installa le librerie richieste (vedi sezione Requisiti).
4.  Apri ed esegui il notebook `progetto.ipynb` utilizzando Jupyter Notebook o Jupyter Lab:
    ```bash
    jupyter notebook progetto.ipynb
    ```

## Risultati

L'analisi condotta nel notebook `progetto.ipynb` ha prodotto diverse informazioni chiave sulla correlazione tra la posizione in qualifica e il risultato finale in gara, con un focus specifico sulla tipologia di circuito.

### Analisi Esplorativa dei Dati (EDA)

1.  **Preparazione dei Dati:** Sono stati uniti e preparati i dataset relativi a circuiti, gare, risultati e classifiche piloti per creare un dataframe analitico comprensivo.
2.  **Distribuzione Posizioni Finali:**
    *   Sono stati generati istogrammi e box plot per visualizzare la distribuzione delle posizioni finali dei piloti, segmentati per le tre tipologie di circuito: "Tecnico", "Alta velocità" e "Misto".
    *   Sono state calcolate le posizioni finali medie per ciascun tipo di circuito, evidenziando come i circuiti "Tecnici" tendano a presentare una media di posizione finale leggermente migliore per i piloti partiti davanti rispetto agli altri tipi.
3.  **Analisi OLAP (Online Analytical Processing) Style:**
    *   È stata esaminata la percentuale di arrivi sul podio in base alla posizione di partenza e al tipo di circuito, rivelando come la posizione di partenza influisca in modo diverso a seconda del tracciato. Ad esempio, sui circuiti "Tecnici", partire nelle primissime file sembra offrire un vantaggio più marcato per l'accesso al podio rispetto ai circuiti di "Alta velocità".

### Test Statistici

*   Sono stati eseguiti test t per confrontare statisticamente le medie delle posizioni finali tra diverse posizioni di partenza (es. P1 vs P2, P2 vs P3) all'interno di ciascuna categoria di circuito. Questi test hanno confermato che, in generale, partire più avanti è associato a una posizione finale media significativamente migliore, sebbene l'entità di questa differenza possa variare con il tipo di circuito.

### Modello di Regressione Logistica

È stato sviluppato un modello di regressione logistica per predire la probabilità che un pilota termini la gara sul podio.

1.  **Features Utilizzate:**
    *   `posizione_partenza` (posizione in griglia)
    *   `classifica_pre_gara_rank` (posizione in classifica del pilota prima della gara, usata come proxy per la "forma" e l'abilità del pilota)
    *   Tipo di circuito, gestito tramite one-hot encoding (es. `circuito_Tecnico`, `circuito_Alta_velocità`, `circuito_Misto`).
2.  **Target:** `podio` (variabile binaria: 1 se il pilota è arrivato sul podio, 0 altrimenti).
3.  **Valutazione del Modello:**
    *   Il modello è stato allenato e validato, e le sue prestazioni sono state confrontate con un modello nullo (baseline).
    *   Sono state calcolate metriche come MAE, MSE, e RMSE. Si raccomanda l'ulteriore analisi con metriche specifiche per la classificazione come Accuracy, Matrice di Confusione, Precisione, Recall, F1-score e curva ROC/AUC per una valutazione più completa.
4.  **Interpretazione dei Coefficienti:** L'analisi dei coefficienti del modello ha permesso di quantificare l'impatto di ciascuna feature sulla probabilità logaritmica (log-odds) di ottenere un podio.
5.  **Test su Nuovi Dati:** Il modello è stato testato su dati di una gara fittizia (`gara04-05-25.csv`) per simulare una predizione su dati non visti, confrontando i risultati predetti con quelli effettivi.

### Conclusioni Preliminari

L'analisi suggerisce che:
*   La posizione di partenza è un fattore cruciale per il risultato finale, ma la sua importanza relativa varia con il tipo di circuito.
*   La "forma" del pilota (approssimata dalla sua classifica pre-gara) è un altro predittore significativo.
*   I modelli di machine learning, come la regressione logistica, possono fornire previsioni utili sulla probabilità di successo in gara basate su questi fattori.

Ulteriori affinamenti del modello e l'esplorazione di altre feature (es. condizioni meteo, affidabilità del team) potrebbero migliorare ulteriormente la comprensione e la capacità predittiva.

*(Questa sezione può essere ulteriormente dettagliata con grafici specifici e metriche precise una volta finalizzata l'analisi nel notebook).*
