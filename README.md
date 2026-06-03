# data_cleaner_class
Python library for Exploratory Data Analysis (EDA) on CSV and pandas DataFrames. It provides utilities for dataset inspection, missing values handling, correlation analysis, distribution testing, and outlier detection.

---

# DataExploration

DataExploration è una libreria Python che semplifica le operazioni di **Exploratory Data Analysis (EDA)** sui dataset gestiti tramite **pandas DataFrame**.

La classe mette a disposizione diversi metodi per analizzare rapidamente la struttura dei dati, individuare valori mancanti, verificare la distribuzione delle variabili numeriche e rilevare eventuali outlier.

## Funzionalità

* Visualizzazione del dataset.
* Informazioni generali sul DataFrame.
* Statistiche descrittive.
* Calcolo della matrice di correlazione.
* Analisi dei valori mancanti.
* Sostituzione automatica di valori mancanti con:

  * media
  * mediana
  * moda
  * forward fill
  * backward fill
  * valore personalizzato
* Individuazione di token anomali utilizzati come missing values (`?`, `NA`, `Unknown`, ecc.).
* Test di normalità tramite **Jarque-Bera**.
* Visualizzazione di istogrammi e boxplot.
* Rimozione degli outlier tramite metodo **IQR (Interquartile Range)**.

## Requisiti

```bash
pip install pandas numpy scipy matplotlib
```

## Utilizzo

```python
import pandas as pd
from data_exploration import DataExploration

df = pd.read_csv("dataset.csv")

data = DataExploration(df)
```

## Esempi

### Informazioni sul dataset

```python
data.get_dataset_info()
```

### Dimensioni del dataset

```python
data.get_dataset_shape()
```

Output:

```python
(1000, 15)
```

### Statistiche descrittive

```python
data.get_dataset_describe()
```

### Correlazione tra variabili numeriche

```python
corr_matrix = data.get_dataset_corr()
print(corr_matrix)
```

### Analisi dei valori mancanti

```python
null_values, missing_percentage = data.get_dataset_missing_values()

print(null_values)
print(missing_percentage)
```

### Sostituzione dei valori mancanti

Con la media:

```python
new_df = data.replace_missing_values(
    method="mean",
    column=["Age", "Salary"]
)
```

Con un valore personalizzato:

```python
new_df = data.replace_missing_values(
    method="fill",
    column=["Age"],
    value=0
)
```

### Test di normalità

```python
results = data.get_dataset_distribution()
print(results)
```

Output:

```python
{
    "Age": {
        "stat": 2.34,
        "p_value": 0.31
    }
}
```

### Istogrammi

```python
data.get_dataset_distribution(mode="hist")
```

### Boxplot

```python
data.get_dataset_distribution(mode="box")
```

### Rimozione degli outlier

```python
clean_df = data.delete_dataset_outliers(
    column=["Age", "Salary"]
)
```

## Gestione automatica dei Missing Values

La libreria riconosce automaticamente diversi valori comunemente utilizzati per rappresentare dati mancanti:

```python
["?", "Unknown", "unknown",
 "NAN", "nan",
 "NA", "na",
 "", " "]
```

Tali valori vengono convertiti in `NaN` prima delle operazioni di analisi.

## Tecnologie utilizzate

* Python
* Pandas
* NumPy
* SciPy
* Matplotlib
