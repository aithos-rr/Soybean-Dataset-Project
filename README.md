# Predizione della Resa della Soia tramite Modelli di Regressione

**Corso:** Intelligenza Artificiale 2 – Sapienza Università di Roma (A.A. 2025/2026)

- Riccardo Romano – 2126461  
- Hera Polegri – matricola 
- Gabriele – matricola

---

## Obiettivo del Progetto

Questo progetto ha l’obiettivo di sviluppare un modello di **Machine Learning supervisionato**
in grado di prevedere la **resa in grano della soia (*Grain Yield, GY*)**
a partire da caratteristiche morfologiche e agronomiche della pianta, insieme a informazioni
di contesto sperimentale come la cultivar e la stagione di crescita.

Il problema affrontato è un caso di **regressione su dati tabellari**, tipico dell’ambito
agronomico, caratterizzato da un numero limitato di osservazioni e da una naturale variabilità
biologica del fenomeno studiato.

---

## Punti di Forza e Metodologia

Il progetto è stato strutturato seguendo un approccio rigoroso e riproducibile, con particolare
attenzione alla corretta modellazione dei dati sperimentali:

1. **Separazione tra Feature Numeriche e Categoriali:**  
   Le variabili di natura diversa sono state trattate in modo appropriato, utilizzando
   *standardizzazione* per le feature numeriche e *one-hot encoding* per le variabili categoriali
   (cultivar e stagione).

2. **Pipeline Completa e Senza Data Leakage:**  
   Tutte le fasi di preprocessing e modellazione sono state incapsulate in oggetti `Pipeline`
   di `scikit-learn`, garantendo una valutazione corretta e riproducibile.

3. **Confronto tra Modelli di Complessità Differente:**  
   Sono stati confrontati un modello lineare regolarizzato (**Ridge Regression**) e un modello
   non lineare (**Random Forest Regressor**) per valutare l’impatto della complessità del modello
   sulle prestazioni predittive.

---

## Dataset

Il dataset utilizzato deriva da uno studio sperimentale agronomico sulle cultivar di soia.

* **Numero di osservazioni:** 320
* **Cultivar:** 40
* **Stagioni di crescita:** 2
* **Repliche sperimentali:** 4 per ciascuna combinazione cultivar–stagione

### Variabili
* **Variabili numeriche:**  
  `PH`, `IFP`, `NLP`, `NGP`, `NGL`, `NS`, `MHG`, `Repetition`
* **Variabili categoriali:**  
  `Season`, `Cultivar`
* **Target:**  
  `GY` – Grain Yield (resa in granella)

> Nota: la variabile `MHG` nel dataset corrisponde al *Thousand Seed Weight (TSW)*
> descritto nel paper di riferimento.

Il file `data.csv` è incluso nella cartella `data/` per garantire la completa riproducibilità
del progetto.

---

## Pipeline del Progetto

Il workflow seguito nel notebook `Soybean_Dataset_Project_Models.ipynb` è il seguente:

1. **Data Loading:** caricamento del dataset e controlli di consistenza.
2. **Problem Definition:** definizione formale di input e target.
3. **Train/Test Split:** suddivisione dei dati (80% training, 20% test).
4. **Preprocessing:** standardizzazione delle variabili numeriche e one-hot encoding delle
   variabili categoriali tramite `ColumnTransformer`.
5. **Baseline Model:** addestramento e valutazione di una **Ridge Regression**.
6. **Non-Linear Model:** addestramento e valutazione di una **Random Forest Regressor**.
7. **Evaluation:** confronto dei modelli tramite MAE, RMSE e R² sul test set.
8. **Model Selection:** selezione e salvataggio del modello migliore.

---

## Risultati Chiave

Il confronto tra i modelli mostra che la **Ridge Regression** ottiene prestazioni
leggermente migliori rispetto alla Random Forest sul test set:

* **MAE (test):** ~277 kg/ha  
* **RMSE (test):** ~350 kg/ha  
* **R² (test):** ~0.53  

La Random Forest non fornisce un miglioramento significativo, suggerendo che,
per questo dataset e in presenza di rumore biologico, una relazione
approssimativamente lineare tra feature e target sia sufficiente a descrivere il fenomeno.

I risultati quantitativi sono disponibili in: results/metrics.csv

