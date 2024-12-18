# README: Cell Data Treatment Classification based on the morphological features

## Overview
This project is an extension of my undergraduate research project, where I monitored changes in the A549 human lung cancer epithelial cell line for 48 hours post-stimulation with different GPCR agonists and **Epidermal Growth Factor (EGF)** using a novel microscopy technique called ptychography that analyses diffraction patterns to produce detailed images of live cells, capturing their size, shape, and behaviour over time. 

**The aim** of this project was to develop an ML model that will be able to differentiate between cells treated with EGF and control based on single cell morphology.

**EGF signalling** is involved in the regulation of cell proliferation, differentiation, division, survival, and cancer development.  EGFRs are tyrosine kinase receptors that activate multiple downstream signalling pathways such as MAPK, (PI3K)/AKT, PKC and Janus kinase/signal transducers and activators of transcription (JAK/STAT) signalling pathways [1] which results in increased cell proliferation, promotes cell survival and inhibits apoptosis [2]. Upregulation of EGFRs often occurs in different cancers e.g. non-small-cell lung cancer, metastatic colorectal cancer, glioblastoma, head and neck cancer, pancreatic cancer, and breast cancer [2].

**Ptychography** provides a unique opportunity to explore in-depth single-cell morphology and behaviour of each cell within a well. Therefore, I wanted to take this project further and explore the effect of EGF on cell morphology features using machine learning. 

**Enjoy! :^)**

### Data Summary:
The experiments were conducted with the following conditions:
- **Cell Line**: A549 (Human Lung Carcinoma Epithelial Cells)
- **Media**: DMEM with 10% FCS for growth; Serum-Free DMEM (SFM) used for washing and control treatment
- **EGF Stimulation**: 75ul of 1nM EGF was prepared and applied to 48-well plate with serum-starved cells to btain final volume of 375ul.
- **Imaging**: Cell images were captured every 30 minutes for 48 hours using a **Phasefocus Livecyte Kinetic Cytometer**.
  
### Key Equipment:
- **Livecyte™ Kinetic Cytometer**: High-sensitivity sCMOS used for live-cell imaging.
- **Environment**: Cells maintained at 37°C with 5% CO2 during imaging.

## Code Description

The code processes cell morphology data, performs data cleaning, builds machine learning models, and evaluates their performance. It generates metrics for comparing classification models and saves the results for further analysis.

### Steps

1. **Data Loading and Cleaning**:
    - The data from **Excel sheets** generated by the Kinetic Cytometer are loaded and cleaned. Each sheet contains measurements of different single cell morphology feature post-treated with SFM or EGF over time.
    - **NaN values** are removed using a custom function (`remove_nans_from_dict`).
  
2. **Dataset Preparation**:
    - The data is compiled into a **single DataFrame**. Features (`X`) include all the parameters except the treatment labels (`y`), which correspond to EGF concentrations or control conditions.
    - The dataset is then split into training and testing sets using `train_test_split`.

3. **Model Training and Comparison**:
    - Three machine learning models are used for evaluation:
        - **Logistic Regression**
        - **K-Nearest Neighbors (KNN)**
        - **Decision Tree Classifier**
    - Cross-validation is performed using `KFold` to compare model performance. A box plot of cross-validation scores for each model is generated.

4. **KNN Pipeline & Hyperparameter Tuning**:
    - A **Pipeline** is created to standardize the features and apply the **K-Nearest Neighbors (KNN)** classifier.
    - Hyperparameter tuning is done using `GridSearchCV` to find the optimal number of neighbors for the KNN model.
  
5. **Model Evaluation**:
    - The best-performing KNN model is evaluated on the test set. Metrics such as the **confusion matrix**, **classification report**, and **ROC AUC score** are generated and displayed.
    - An **ROC curve** is plotted to visualize the trade-off between the true positive rate and false positive rate for predicting EGF treatment.

6. **Results Saving**:
    - All results, including cross-validation scores, best hyperparameters, confusion matrix, classification report, and ROC AUC score, are saved into a text file (`model_evaluation.txt`).
    - Plots (model comparison and ROC curve) are saved as image files in the `results` folder.

### Results
- **Model Performance**: The KNN classifier was optimized through hyperparameter tuning, achieving the best performance among the models.
- **Best Parameters**: The optimal number of neighbors (`n_neighbors`) for KNN was selected.
- **ROC Curve**: The ROC curve showed the classifier's ability to differentiate between treated and untreated cells.
- **Evaluation Metrics**: The model's accuracy, precision, recall, and other metrics were reported for evaluating the classifier's prediction performance.


## How to Run the Code
1. Ensure that the `cell_morphology_data.xlsx` file is present in the working directory.
2. Run the script in a Python environment to process the data, train models, and generate results.
3. The output files (model performance plot, ROC curve, and evaluation metrics) will be saved in the `results` folder.

## Conclusion
This project showed how machine learning can be applied to analyse cellular responses to EGF stimulation based on the morphological data generated with ptychography. From different ML models, the KNN classifier showed the best performance and was further optimised through hyperparameter tuning. The optimised KNN model successfully predicts the cell’s treatment condition (SFM vs. EGF), achieving a cross-validation score of 0.7727 and an overall ROC AUC score of 0.712, which indicates an acceptable model’s performance.

## Contact
If you have any questions, feel free to reach out! 
- **Email**: [alicja.ziajowska@gmail.com](mailto: alicja.ziajowska@gmail.com) 
- **GitHub**: [a-ziaj](https://github.com/a-ziaj) 
- **LinkedIn**: [Alicja Ziajowska]( https://www.linkedin.com/in/alicja-ziajowska-b8a977180/)

## References
1.	Wee, P., & Wang, Z. (2017). Epidermal growth factor receptor cell proliferation signaling pathways. Cancers, 9(5), 52. https://doi.org/10.3390/cancers9050052 
2.	Wei, Q., Costanzi, S., Balasubramanian, R., Gao, Z.-G., & Jacobson, K. A. (2013). A2B adenosine receptor blockade inhibits growth of prostate cancer cells. Purinergic Signalling, 9(2), 271–280. https://doi.org/10.1007/s11302-012-9350-3 




