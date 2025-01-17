# Tanzania Water Project

## Premise: 

Aqua partners is a public sector consulting firm which helps governments improve water access for their populations. This project is done in cooperation with the Government of Tanzania and the minister of water and irigation. 

## Data & Objective:

We are using a dataset containing all the existing water pumps in the country. Associated with each water pump is a series of features such as: Date of installation / Water quality / Region / Installing Organisation / Source type / Nearest water bassin
Length of operation. We are aiming to use classification algorithms to evaluate the features that determine whether a water pump works or not. Provided the classification yields high predictive performance we will be able to recommend to the Tanazanian government which features drive the usability of a water pump. This will also enable them to select and evaluate more carefully third parties who install water pumps (World Bank, Anglican Church, Charities). 


## Data Structure, Selection & Transformation:

The raw dataset contains 60,000 water pumps and 41 different features. Combining feature selection and engineering we reduced the dataset to 29 features prior to binary transformation. We are using Functional / Non-Functional as our target. We made some additional small features changes to simplify the dataset detailed in the Main jupyter notebook. We used undersamping to fix class imbalance across the existing set of water pumps to avoid overfitting. Our end dataset contains 869 features after binary transformation. 

Train-Test split: 80/20 

K-fold cross validation: 5 folds / stratified random sampling

## Modeling

Model Scoring measure(s): Accuracy
Hyperparameter optimisation: GridSearch CV

Baseline Model (Train / Validation):

           - Decision Tree: 0.90 / 0.77

![](images/tree.png)

Secondary Models (Train / Validation): 

          - Logistic Regression: 0.78 / 0.77 
          
          - Random Forest: 0.77 / 0.76
          
          - Support Vector Machines: 0.50 / 0.49
          
          - K-nearest-neighbors: 0.68 / 0.69
          
          - Ensemble Methods: 
              
              - Logistic Regression w/ Bagging: 0.78 / 0.77
              
          - Hyperparameter optimisation: 
          
              - Decision Tree: 0.90 / 0.86

## Final Model Selection & Test Performance

We chose the Decision Tree with parameter optimization as our final model. 

Final Model (Train / Validation / Test): 

           - Decision Tree (Max depth = 40 / Min samples leaf = 20)
                      
                      - Accuracy: 0.90 / 0.86 / 0.86


![](images/final_model_params.png)

## Interpretation 

The model we have chosen should enable us to predict and influence the outcome of future water pumps. The features below are the main driver of the model outcome. We recommend the government of Tanzania to use the factors below in their discussions with third parties who are building pumps and challenge them on their assessment of these features. This will improve the future usability of exiting and new pumps and insure their usability over a long period. 

The determinants of the usability of a waterpump include:
          
          - water quality

          - quantity of water available
          
          - gps height (altitude of the well) 
          
          - length of operation

### Threshold Selection for Optimum Model

We selected a threshold for our stakeholders using the following metrics (a positive being a functional water pump and a negative being a non-functional water pump):

           - cfp = 100

           - ctn = 50

           - cfn = 0

           - ctp = -50

The rational for this was that a true positive, a functional water pump correctly identified would have the lowest score, a true negative would have a cost of repairing the pump associated with it. The most costly would be a false positive, a non functional water pump classified as functional, as this would have health and wellness implications for the population dependent upon it, as well as any repair costs. The cost of a false negative was set to 0 as a benchmark.

### Top 10 features:

![](images/features_final.png)


### Recommendations

Based on the model results and feature weights we recommend that the minister of water and irigation deploy resources to conduct additional due diligence on water sources where wells are being installed. In addition, there is strong evidence of lack of functionality for wells installed at higher levels. We suggest adding using government oversight to make sure wells are installed at lower levels where possible. Our final recommendation is to setup a new fund / organisation to review and repair older wells in cooperation with non-governmental organisations assisting with wells construction. 
