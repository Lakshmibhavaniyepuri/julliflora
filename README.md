This project implements a Juliflora vs Non-Juliflora classification system using Sentinel-2 SR imagery (Aug–Nov 2023) in Kanigiri region. The workflow applies Principal Component Analysis (PCA) for dimensionality reduction and uses three machine learning classifiers:

Support Vector Machine (SVM)
Random Forest (RF)
Gradient Tree Boosting (GTB)

The script performs training/testing splits, accuracy assessment (confusion matrix, precision, recall, F1-score, RMSE), visualization, and area estimation of Juliflora spread. Final results are exported as GeoTIFFs to Google Drive.

🛰️ Data Used

Satellite Data: Sentinel-2 Surface Reflectance (COPERNICUS/S2_SR_HARMONIZED)
Time Period: August 1 – November 30, 2023
Cloud Filter: < 1% cloud cover
Bands Used in PCA: B4 (Red), B8 (NIR), B8A (Narrow NIR), B12 (SWIR2)
AOI: Kanigiri region (imported as FeatureCollection)

⚙️ Workflow
1. Data Preprocessing
Filter Sentinel-2 SR imagery,Apply cloud filter,Mosaic using median composite and Clip to AOI

2. Dimensionality Reduction (PCA)

Standardize selected bands (B4, B8, B8A, B12) , Compute covariance and eigen decomposition, Generate PC1–PC4 components

3. Training Data Preparation

Two classes:
1 → Juliflora
0 → Non-Juliflora

Merge FeatureCollections for training
Split into 80% training and 20% testing

4. Classification

Train models:
SVM (libsvm)
Random Forest (100 trees)
Gradient Tree Boosting (100 trees)
Apply classification on PCA bands

5. Accuracy Assessment

Confusion Matrix
Accuracy
Precision, Recall, F1-score
RMSE

6. Area Estimation

Extract Juliflora mask (class = 1)
Multiply with pixel area
Sum over AOI to estimate Juliflora spread (sqm)

7. Export Results

Classified maps (SVM, RF, GTB) exported to Google Drive as GeoTIFF
Folder: Juliflora_PCA_Export

🎨 Visualization
True Color Composite (B8-B4-B3) for Sentinel-2 mosaic
PCA Image (PC1–PC3) visualization

Classified outputs:
Blue → Juliflora (SVM)
Green → Juliflora (RF)
Yellow → Juliflora (GTB)

Interactive legend added to map

📊 Outputs
Accuracy reports (Confusion Matrices, Precision, Recall, F1, RMSE)
Estimated Juliflora area (sqm)
Classified GeoTIFF maps for SVM, RF, GTB


🚀 How to Run
Open Google Earth Engine Code Editor
Import your AOI (table FeatureCollection).
Import julliflora and nonjulliflora training shapefiles.
Copy and paste the script into the Code Editor.
Run the script → check map layers and printed accuracy metrics.
Exports will be saved to your Google Drive.

📌 Notes
Adjust AOI path based on your GEE assets.
Modify training data (julliflora, nonjulliflora) before running.
Change classifier masks in area estimation if you want area from RF or GTB.
