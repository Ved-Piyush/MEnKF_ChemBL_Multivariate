# MEnKF_ChemBL_Multivariate
Matrix Ensemble Kalman Filter for Multivariate Target Prediction using the Chembl database

## Data Preparation

1. Download the datasets [No_Filters.csv]() , [Small_Molecule_Phase_3.csv](https://drive.google.com/file/d/1BcG5A3Af6GncJoDptH8cLe5AkXbrPqTm/view?usp=sharing) and place in the [Data](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/tree/main/Data) folder.

2. Run the script [Combine_Small_and_Big_Datasets.ipynb](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/blob/main/Data_Preparation/Combine_Small_and_Big_Datasets.ipynb) that will create the file `combined_data.csv` in the [Data](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/tree/main/Data) folder.

3. Run the script [Make_Rdkit_Features.ipynb](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/blob/main/Data_Preparation/Make_Rdkit_Features.ipynb) which will map the Rdkit features to the Smiles in the `combined_data.csv` dataset. It will then create a file called `combined_data_with_rdkit.csv` in the [Data](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/tree/main/Data) folder.

4. Run the script [Train_Test_Splits.ipynb](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/blob/main/Data_Preparation/Train_Test_Splits.ipynb) which will create the files `x_train.csv`, `x_valid.csv`, `y_train.csv`, `y_valid.csv`, `smiles_with_rdkit_with_small_phase_3_features.csv`, and `smiles_with_rdkit_with_small_phase_3_outputs.csv` in the [Data](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/tree/main/Data) folder. In this script the multivariate targets `y_train.csv` are standardized to have a column mean and standard deviation of 0 and 1, respectively. The standardizer object will be placed in the [Data](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/tree/main/Data) folder by the name of `std_scaler.pkl`. 

5. Train the multi-arm base model using the script [PSA_AlogP_Base_Model.ipynb](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/blob/main/Base_Model_Training/PSA_AlogP_Base_Model.ipynb). The stored model `Model_BOTH` will be placed in the [Base_Models](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/tree/main/Base_Models) folder. 
