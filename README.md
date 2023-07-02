# MEnKF_ChemBL_Multivariate
Matrix Ensemble Kalman Filter for Multivariate Target Prediction using the Chembl database

## Data Preparation

To create the feature files to run the Matrix Ensemble Kalman Filter Method please follow the following steps. On following steps 1 through 6 you will get many interim files which will be required to create the final feature file 

1. Download the datasets [No_Filters.csv]() , [Small_Molecule_Phase_3.csv](https://drive.google.com/file/d/1BcG5A3Af6GncJoDptH8cLe5AkXbrPqTm/view?usp=sharing) and place in the [Data](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/tree/main/Data) folder.

2. Run the script [Combine_Small_and_Big_Datasets.ipynb](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/blob/main/Data_Preparation/Combine_Small_and_Big_Datasets.ipynb) that will create the file `combined_data.csv` in the [Data](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/tree/main/Data) folder.

3. Run the script [Make_Rdkit_Features.ipynb](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/blob/main/Data_Preparation/Make_Rdkit_Features.ipynb) which will map the Rdkit features to the Smiles in the `combined_data.csv` dataset. It will then create a file called `combined_data_with_rdkit.csv` in the [Data](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/tree/main/Data) folder.

4. Run the script [Train_Test_Splits.ipynb](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/blob/main/Data_Preparation/Train_Test_Splits.ipynb) which will create the files `x_train.csv`, `x_valid.csv`, `y_train.csv`, `y_valid.csv`, `smiles_with_rdkit_with_small_phase_3_features.csv`, and `smiles_with_rdkit_with_small_phase_3_outputs.csv` in the [Data](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/tree/main/Data) folder. In this script, the rdkit features are standardized to have a column mean and standard deviation of 0 and 1, respectively. The standardizer object will be placed in the [Data](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/tree/main/Data) folder by the name of `std_scaler.pkl`. 

5. Train the multi-arm base model using the script [PSA_AlogP_Base_Model.ipynb](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/blob/main/Base_Model_Training/PSA_AlogP_Base_Model.ipynb). The stored model `Model_BOTH` will be placed in the [Base_Models](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/tree/main/Base_Models) folder. The multivariate targets are standardized to have column means and standard deviation of 0 and 1, respectively. The standardizer object can be found in the [Data](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/tree/main/Data) folder by the name of `target_scaler.pkl`.

6. Use the trained multi-arm base model from 5 to extract the smiles and rdkit embeddings for the samples in the `smiles_with_rdkit_with_small_phase_3_features.csv` dataset using the script [Extract_BottleNeck_Features_Both.ipynb](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/blob/main/EnKF_Yegenoglu/Extract_BottleNeck_Features_Both.ipynb). The extracted embeddings will be in a file called `small_mol_phase_3_features_for_both.npy` in the [Data](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/tree/main/Data) folder.

## Running the MEnKF method

1. Run the script [Yegenoglu_Method_Learnable_Covariance_using_Script_Ht_try_other_values_subscript_in_ys](https://github.com/Ved-Piyush/MEnKF_ChemBL_Multivariate/blob/main/EnKF_Yegenoglu_Script_H_t/Yegenoglu_Method_Learnable_Covariance_using_Script_Ht_try_other_values_subscript_in_ys.ipynb) which will run the MEnKF method on the features `small_mol_phase_3_features_for_both.npy` and outputs `smiles_with_rdkit_with_small_phase_3_outputs.csv`. Towards the end of the script, one can find the evaluation metrics of root mean squared errors, coverages, and widths of the prediction intervals for the training and the testing sets. There are also the observed vs. predicted scatterplots for the testing data and the trajectory of the convex averaging weights over the updating iterations. There's also a plot of the histogram of the predictions from MEnKF method for some test samples along with the ground truth value and the empirical 95% prediction intervals from the MEnKF method. 


