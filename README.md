# README: Obligatorisk Aflevering 1: Regressionsanalyse og Klassifikation

Dette projekt indeholder den komplette løsning og dokumentation for Obligatorisk Aflevering 1, som er baseret på analyse af bilers brændstofeffektivitet ved brug af maskinlæringsmodeller.

## 1. Projektoversigt og Mål

Hovedformålet med opgaven var at formulere, træne og finjustere modeller for to distinkte statistiske problemer:

1.  **Regressionsproblem:** At forudsige bilens kontinuerlige brændstofeffektivitet (`mpg`) baseret på features som vægt, hestekræfter og cylinderantal.
2.  **Klassifikationsproblem:** At forudsige, om en bil er "højeffektiv" (`mpg` > median) eller "lav-effektiv" ved hjælp af logistisk regression.

Finjusteringen af modellerne (Ridge, Lasso og Logistisk Regression) blev udført ved hjælp af Pipeline og krydsvalideringsteknikker for at sikre robusthed i resultaterne.

## 2. Projektfiler og Struktur

Alle projektfiler er inkluderet i dette repository.

| Fil/Mappe | Beskrivelse | Note |
| :--- | :--- | :--- |
| `notebooks/notebook.ipynb` | Hovedfilen med al Python-kode, dataforberedelse, træning og finjustering af modeller (Lineær, Ridge, Lasso, Logistisk Regression). | Skal indsendes. |
| `articles/article.tex` | LaTeX-kildefilen for den maksimale to-siders forskningsartikel. | Skal indsendes. |
| `articles/article.pdf` | Det færdige, kompilerede dokument. | Skal indsendes. |
| `models/` | Indeholder alle genererede visualiseringer (f.eks., ROC Curve, Confusion Matrices, Ridge vs Lasso plots). | Alle plots skal indsendes. |
| `data/` | Mappen hvor datafilen skal placeres for at køre notebook'en. | Mappen skal inkluderes, men datafilen skal undlades (se Sektion 3). |


## 3. Datafremskaffelse og Forberedelse

**Dette repository indeholder ikke den rå datafil.**

For at genskabe analysen skal filen **`cars.csv`** først fremskaffes fra kursusmaterialemappen i kursusmaterialets repository.

**Opsætning:** Når filen er indhentet, skal den placeres i en undermappe kaldet `/data/` i roden af projektet.

**Forberedelse i Notebook:**
1.  CSV-filen indlæses, og manglende værdier (`?`) erstattes med `pd.NA`.
2.  Relevante kolonner konverteres til numeriske datatyper.
3.  Rækker med manglende værdier fjernes (`dropna`).
4.  Datasættet opdeles én gang (80/20 split) til både regressions- og logistisk regression.

## 4. Anvendte Metoder og Finjustering

| Problem | Baseline Model | Finjusteringsmetoder |
| :--- | :--- | :--- |
| **Regression** (`mpg`) | Lineær Regression | RidgeCV, LassoCV [10, 11]. Brug af `Pipeline` med `StandardScaler` og `GridSearchCV`. |
| **Klassifikation** (`high_efficiency`) | Logistisk Regression | Logistisk Regression med **LogisticRegressionCV** for at optimere regulariseringsparameteren $C$. |

## 5. Hovedresultater

Resultaterne er baseret på de finjusterede modellers ydeevne på testsættet:

### Regressionsanalyse
*   **$R^2$ Score:** Både Lineær, Ridge og Lasso opnåede en $R^2$ score på ca. **0.817** på testsættet.
*   **Konklusion:** De finjusterede modeller præsterer meget ligeligt og bekræfter modellernes stærke prædiktive evne.

### Klassifikationsanalyse
*   **AUC Score:** Den finjusterede logistiske regressionsmodel opnåede en fremragende AUC (Area Under the Curve) på **0.95**. Dette indikerer en høj evne til at adskille klasserne.
*   **Forvirringsmatrix (Confusion Matrix):** Den finjusterede model opnåede **36 True Negatives** og **36 True Positives**. Kun 7 af de 79 testeksempler blev fejlklassificeret (1 False Positive, 6 False Negatives)
