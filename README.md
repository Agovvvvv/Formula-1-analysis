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

## Risultati (Da completare)

*(Questa sezione può essere aggiornata con i grafici chiave, le scoperte principali e le conclusioni dell'analisi una volta completata).* 
