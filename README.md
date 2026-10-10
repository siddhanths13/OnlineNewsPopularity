# NewsSpace

NewsSpace is a responsive, browser-side Linear Algebra workspace for UCI Online News Popularity. It explores the dependency structure of the fixed feature columns, then compares reduced representations for held-out least-squares prediction.

## Official project dataset

**Load Official Dataset** reads the bundled [`data/online-news-popularity-seed-2025-800.csv`](data/online-news-popularity-seed-2025-800.csv). It contains exactly 800 rows selected reproducibly with seed 2025 from the linked UCI archive CSV, with 58 predictive features and the `shares` target. Use an HTTP static server (for example, `python3 -m http.server`) so the browser can fetch the bundled file. The full archive can also be downloaded from the [UCI dataset page](https://archive.ics.uci.edu/dataset/332/online%2Bnews%2Bpopularity) and selected with **Choose Full UCI CSV**.

There is a source count discrepancy: UCI's dataset listing says 39,797 instances, while the CSV inside the linked archive contains 39,644 data rows. The bundled sample is selected from those 39,644 actual rows. NewsSpace displays this distinction and never creates the missing rows.

The downloaded data is licensed CC BY 4.0. Attribution: Fernandes, Vinagre, Cortez, and Sernadela, *Online News Popularity*, UCI Machine Learning Repository, DOI [10.24432/C5NS3V](https://doi.org/10.24432/C5NS3V).

The 58 predictive feature definitions are shared by every article. Each row supplies different values for those same columns.

## Explore another dataset

Upload a CSV with a header row and numerical observation columns. Text columns are excluded and listed; the target is explicitly selectable. Missing feature/target rows are reported and omitted from the calculation. Constant columns are identified and deselected initially. Around 50–1,000 rows are preferred.

## Mathematics

All results are calculated in the browser after selecting **Run Linear Algebra Analysis**. Rank and pivot columns come from column-pivoted modified Gram–Schmidt on standardized feature columns, with a scale-aware floating-point tolerance. PCA uses the sample covariance matrix and a symmetric Jacobi eigensolver. Regression metrics use a deterministic first-80% / final-20% split.

The original-feature basis consists of selected columns in sample space (each feature is a vector across the articles). PCA components are new feature-space directions. The article inspector shows original feature values and actual PCA coordinates. Prediction metrics are shown only when least-squares fitting succeeds; without a target, structural analysis still works.

## Run

Serve this directory with a static HTTP server. No Python API or build step is required.
