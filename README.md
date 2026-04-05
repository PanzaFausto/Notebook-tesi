# Tecniche di Machine Learning per Indoor Positioning 🏛️📱

[![Python](https://img.shields.io/badge/Python-3.12-blue.svg)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-1.6.1-orange.svg)](https://scikit-learn.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-2.x-green.svg)](https://xgboost.readthedocs.io/)

Repository ufficiale del codice sorgente e degli script di analisi per la tesi di Laurea Magistrale in Ingegneria Informatica: **"Tecniche di Machine Learning per Indoor Positioning"** (Università degli Studi Roma Tre).

**Autore:** Alessio Prete

---

## 📖 Abstract
Questo progetto affronta il problema della localizzazione indoor in ambienti museali complessi (Gallerie Nazionali di Palazzo Barberini, Roma) utilizzando la tecnologia **Bluetooth Low Energy (BLE)** e algoritmi di **Machine Learning**. 

L'obiettivo è superare i limiti degli approcci geometrici classici (come il *k-NN*) introducendo modelli avanzati (come il **Random Forest** e **XGBoost**) capaci di gestire il rumore del segnale radio, i fenomeni di multipath e l'eterogeneità hardware dei dispositivi (Android vs iOS). Il sistema dimostra una resilienza eccezionale ai guasti infrastrutturali (*Graceful Degradation*) ed esplora l'efficacia della *Sensor Fusion* tramite sensori inerziali.

---

## 📂 Struttura del Repository
Il codice è interamente sviluppato in Python tramite notebook interattivi, eseguiti in ambiente Google Colab. I 20 script sono suddivisi in quattro macro-categorie:

### 1. Preparazione Dati e Feature Engineering
*   `BAR_Fingerprint_Mediana`: Creazione dei dataset di fingerprint con aggregazione a mediana dinamica.
*   `BAR_Sensor_Fusion`: Integrazione dei dati inerziali (IMU) con le scansioni radio.
*   `Accelerometro_Giroscopio-cap4`: Estrazione di feature statistiche dai log dei sensori inerziali.

### 2. Addestramento e Valutazione Modelli
*   `BAR_Positioning_RandomForest`: Ottimizzazione iperparametri (Grid Search) e 10-Fold CV per il Random Forest.
*   `BAR_Positioning_Baseline`: Valutazione delle baseline geometriche (1-NN, 57-NN) e di prossimità.
*   `BAR_Positioning_LogisticRegression`: Addestramento del modello lineare.
*   `Calcolo Accuratezza Logistic Regression-cap4`: Valutazione della complessità e linearità dello spazio vettoriale.
*   `BAR_XGBoost_Experiment`: Esperimento comparativo con lo stato dell'arte (XGBoost).
*   `Analisi Cross-Platform_cap4`: Valutazione del *Domain Shift* e metriche incrociate Android/iOS.
*   `BAR_Analisi_Anomalie`: *Anomaly Injection* e stress test sull'infrastruttura (simulazione beacon guasti).
*   `BAR_Compare_Mean_vs_Median`: Analisi quantitativa dell'aggregazione a media vs mediana.

### 3. Validazione Statistica
*   `BAR_Validazione_Scientifica`: Esecuzione del Paired T-Test per certificare la superiorità del Random Forest.
*   `BAR_Validazione_Statistica_Finale`: Calcolo riassuntivo di tutti i p-value riportati nella tesi.

### 4. Generazione Grafici e Strutture Visive
*   `BAR_Analisi_CrossPlatform`: Boxplot dell'offset sistematico RSSI tra dispositivi.
*   `Analisi-Importanza-Feature_cap4`: Estrazione istogramma della *Feature Importance* (MDI).
*   `confusion_matrix`: Generazione heatmap delle matrici di confusione.
*   `robustness_curve`: Plot delle curve di *Graceful Degradation*.
*   `pipeline_schema_generator`: Schema vettoriale (Graphviz) della pipeline di localizzazione.
*   `gradient_boosting_schema_generate`: Schema logico dell'addestramento additivo.
*   `gini_split_diagram_generate`: Illustrazione del partizionamento di un nodo basato sull'impurezza di Gini.

---

## 📊 Dataset
Gli script utilizzano i dati estratti dal dataset **BAR (Barberini Art Recognition)**, raccolto originariamente a Palazzo Barberini su 93 beacon iBeacon e 90 opere d'arte. Il dataset comprende sessioni di scansione indipendenti catturate simultaneamente con dispositivi Android (Samsung Galaxy S21) e iOS (iPhone 16).

---

## 🏆 Risultati Principali
Accuratezza Intra-Device: Il Random Forest raggiunge un'accuratezza del 99.78%, superando la baseline k-NN del +12.7 p.p.

Robustezza ai Guasti: Il sistema mantiene un'accuratezza >84% anche a fronte di un collasso infrastrutturale dell'11% dei sensori.

Sensor Fusion: Il Ceiling Effect dimostra che l'uso dei sensori inerziali apporta un guadagno trascurabile (+0.07%), validando la scelta energeticamente efficiente del solo segnale radio BLE.

Il "Paradosso iOS": Nonostante l'aggressivo risparmio energetico dei dispositivi Apple causi un crollo dell'identificazione esatta (Top-1 al 66%), la Top-3 Accuracy rivela che l'opera cercata è nel vicinato probabilistico quasi nel 94% dei casi.

---


## 🚀 Setup e Requisiti
Tutti gli script sono stati ideati per essere eseguiti all'interno di Google Colab, sfruttando l'archiviazione su Google Drive.

Per eseguire localmente i notebook, è necessario installare le seguenti dipendenze:
```bash
pip install pandas numpy scikit-learn xgboost matplotlib seaborn scipy graphviz
