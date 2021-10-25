# Building Application Introduction
Building Applications are widely used in building energy tracing, fault detection and equipment control, which are always developed in data-driven manner today. Here, we firstly introduce the application named **Energy Consumption Predition (ECP)**, and then show how two different building datasets can be used for this application.
## Energy Consumption Prediction
The Energy Consumption Prdiction can be used to predict the next timestamp energy consumption of a group of building systems by training a ML model with histrical electricity data of the related systems. Here, a general ML model construction process can be followed to get this model, which consists of data access, data processing, model training, model evaluation orderly.
## Public Building Datasets
Besides the EMSD data, we also provide an open-source dataset from project [**Genome**][genome]. Both of them can be used for training ECP models and downloaded [**here**][download].
## Model Introduction
### Model 1
Model 1 is a [Random Forest][RF] model which using the historical data from various systems of the building (e.g., chilled water system and hot water system) and solar illuminance data to train an ML model.
### Model 2
Model 2 is a [LSTM][LSTM] model which using the time-series data from both electrical and non-electrical systems and the weather data to train a neural network.
## Example: Using Genome Data with Energon
By writing EnergonQL, [**Energon**][energon] can assist to access the **Genome** data. For example:

`SELECT (Chilled_Water + Hot_Water) * Flow_Rate + Solar * Illuminance`\
`FROM Building A`\
`WHERE A.id = 'Genome'`

This query extracts the following list of features in **Genome**:

+ **Chilled Water Flow**
+ **Hot Water Flow**
+ **Solar illuminance**

By using these features as input of model 1, the accuracy of model 1 for **Genome** is 58% with the **percentage error** as metric.


You can find the implement codes [**here**][download2] and try it by yourself.
```
project
│   README.md
│   file001.txt    
│
└───folder1
│   │   file011.txt
│   │   file012.txt
│   │
│   └───subfolder1
│       │   file111.txt
│       │   file112.txt
│       │   ...
│   
└───folder2
    │   file021.txt
    │   file022.txt
```
## Cogitation 1
How can we write **EnergonQL** queries to extract the followling list of features of **Genome** data for Model 2?

+ **Chilled Water Flow**
+ **Hot Water Flow**
+ **Solar Illuminance**
+ **Outdoor Temperature**
+ **Building Electricity**

**Solution:**

`SELECT Power + (Chilled_Water + Hot_Water) * Flow_Rate + Solar * Illuminance + Weather * Temperature`\
`FROM Building A`\
`WHERE A.id = 'Genome'`

The evaluation result show that these features for Model 2 increasing the accuracy to **85%**.

You can find the implement codes [**here**][download2] and try it by yourself.
## Cogitation 2
How can we write **EnergonQL** queries to extrac the followling list of features of **EMSD** data for Model 1?
+ **AHU Electricity**
+ **Chiller Electricity**
+ **Outdoor Temperature**

**Solution:**

`SELECT (Chiller  + AHU) * Power + Weather * Temperature`\
`FROM Building A`\
`WHERE A.id = 'Genome'`

By using these features as input of model 1, the accuracy of model 1 for **EMSD** is 71% with the **percentage error** as metric.



[genome]:https://github.com/buds-lab/the-building-data-genome-project
[brick]:https://brickschema.org/ontology/
[energon]:https://github.com/fangger4396/energon_example/blob/main/Energon.md
[download]:https://github.com/fangger4396/energon_example/blob/main/cement.md
[RF]:https://www.sciencedirect.com/science/article/pii/S0378778818311290
[LSTM]:https://www.sciencedirect.com/science/article/pii/S0306261917302921
[download2]:https://drive.google.com/file/d/1EwPoNCn1O0-ag71p_tIN1DbzSfLc1VFl/view?usp=sharing
