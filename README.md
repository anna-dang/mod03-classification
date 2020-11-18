Flatiron Data Science Program

Module 3 Project - Classification

November (Friday the) 13 , 2020

---

# *Pump It Up!*

*Data Mining the Water Table*

<img alt="woman fills bucket at a water point" src="/images/woman_well.jpg" width="800"/>

---

### Overview

Tanzania, as a developing country, struggles with providing clean water to its population of over 57,000,000. There are many waterpoints already established in the country, but some are in need of repair while others have failed altogether. A smart understanding of which waterpoints will fail can improve maintenance operations and ensure that clean, potable water is available to communities across Tanzania.

Objective: Build a classifier to predict the condition of a water well. This is a **ternary** classification problem, water points may be listed as: Funtional, Non-Functional, or Functional (Needs Repair).

Repository Contents:
    - data : competition data and cleaned/transformed data as CSV files
    - images : images for display through this analysis
    - notebooks : full analysis documentation
    - predictions : model predicted labels for submission to the competition
    - README.md : project summary and contents
    - Mod03_presentation.pdf : presentation slides with comments

---

### Data

Cleaning notebooks: Modeling data [cleaning](/notebooks/data_cleaning.ipynb) and validation set [transformation](../notebooks/validation_transformation.ipynb)

This dataset is part of an *active competition* until April 31, 2021 from [DRIVEN DATA](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/page/23/). No outside data was permitted to be used.

validation_transformation.ipynb

### EDA/Conclusions

#### 1) What is the Waterpoint Geographical Distribution?

Full analysis: [Question 1 Notebook](/notebooks/question_1_waterpoint_distribution.ipynb)

![seperate mao](/images/sep_dist.png)

Location can be a predictor of well status, typically as it relates to the Rural Access Index (RAI).

#### 2) Does seasonality effect status (season of evaluation)?

Full analysis: [Question 2 Notebook](/notebooks/question_2_seasonality.ipynb)

![seasonality and rainfaill](/images/seasons.png)

Pumps are more likely to be functional after wet season has been past. 

During the other times the reporting is much more equal.


#### 3) Waterpoint management relationship to status?

Full analysis: [Question 3 Notebook](/notebooks/question_3_management.ipynb)

![management bar graph](/images/management.png)

Wells managed by legal entities:
  
     - VWC
     - WUA
     - The Water Board
     
have the greatest percentage of functional wells.

![payment bar graph](/images/payment.png)

Wells that require payment are more likely to be functional.


### Classifier

Full analysis: [Modeling Notebook](/notebooks/modeling.ipynb)

Accuracy was the set metric to optimize for by the competition. Accuracy makes sense as a metric for this application because it is a better gauge of whether the model is discerning the rare class than others. 

The best performing model was an XGBClassifier with the following parameters: 
    learning_rate=0.2, 
    max_depth=6, 
    min_child_weight=2,
    objective='multi:softprob',
    subsample=0.7

Competition performance: **77.97% accuracy** of predictions for the validation set upon submission to the competition. 

Model fitness: The modeling test set scored **77.63%** accuracy. Only **0.34%** difference, indicating the model is fit well and not over trained. 

Current limits: The model is having difficultly discerning 'functional' from the rare class 'functional, needs repair'. Attempts to correct for class imbalance resulted in significant overfitting, with little gain in rare class predictions.

Important feature groups:

    - 'quantity' : 'dry'
    - 'water_point_type' : 'other'
    - 'extraction_type' : 'other'
    - 'management_type'
    - 'region'

<img alt="submission score" src="/images/score.png" width="400"/>

<img alt="confusion" src="/images/confusion.png" width="600"/>

    
---

### Reccomendations

    - Expand notice at non-functional water points to the nearest functional point. 
    - Consider repair/replace pumps in areas with lowest RAI first.
    - More funding or management assistance to the sub-village level to help them manage and repair their non-payment wells. 


#### Future Work

    - Tease appart the 'other' value category for important features for the current model.
    - Research'functional' wells beyond whether they 'work' to see if they are actually potable and supplying enough water to the local population.
    - Investigate a further breakdown of failing management entities.
    - A different strategy: Since correcting the imbalance for the rare class did not improve the model, perehaps explore model stacking. First binary between 'functional' and 'non' and then between between 'functional' and 'needs repair'.


#### Thank you for viewing my project!

Please review the full analysis in the [Notebooks](/notebooks) folder or view my presentation [slideshow](/Mod03_presentation.pdf) or [video]().



