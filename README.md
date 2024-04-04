# ML-Causal-Inference

<div align="justify"> 
  
This notebook aims to estimate the causal effect of Ozempic on obese and hypertensive patients. Specifically, we seek to quantify the change in outcomes associated with Ozempic use compared to a control group or baseline. By assessing the causal effect of Ozempic, we gain insights into its potential benefits and harms for this patient population. These insights can help in clinical decision-making and improve patient outcomes.

Let’s first understand these methodologies

**Double Lasso :**
Since observational studies are not randomised, there will be a lot of confounding variables effecting treatment & response, which have to be controlled for.
We do that by adding all the confounders to the equation. We estimate causal effect by performing double lasso, controlling for confounders using regression
- 1st on treatment - helps select a subset of confounders that are most relevant for predicting the treatment
- 2nd on outcome variable - selected subset of confounders from the first stage, along with the treatment variable, as predictors.

**Steps :**

**Data Preparation :** The notebook begins by importing the necessary libraries and loading the dataset.
- Medical dataset :
    - 9.67 % of the records are duplicated in this case, which are then dropped
    - Within one encounter, patients can have multiple procedures
    - dataset has prescription different drugs, filter for ozempic, proc_code == 'J3490'
    - Missing Values : evaluate the ratio of missing values in the dataset & impute the values with 0 , mean , mode & unknown
    - Create flags for Obesity & hypertension by filtering for 'E669' & 'I11*' diagnosis codes
    - Label encoding categorical variables

**Model : Double Lasso**
- Create a flag to capture the outcome of the treatment. for patients diagnosed with hypertension/obesity, check if their further diagnosis (next visit) continue to have hypertension/obesity, if not then the patient is cured.
- Train test split
- 1st Stage : Regress all the X variables on treatment to get the list of significant confounding variables
- 2nd Stage : Regress treatment, along with all the confounding variables(un penalised) found in stage 1 & remaining X variables (penalised), to get all the significant variables effecting the outcome (cured/not cured)

**Model Evaluation :**
- R^2 of -0.346 suggests that the model does not capture the underlying patterns in the data well and that the data has a high degree of variability that cannot be well-predicted by a linear model
- Model is not the correct choice for this type of data

Contributions Feel free to submit pull requests or start an issue if you find a bug or have any suggestions for improving this notebook.
</div>
