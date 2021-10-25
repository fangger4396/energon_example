# Building Application Introduction
Building Applications are widely used in building energy tracing, fault detection and equipment control, which are always developed in data-driven manner today. Here, we firstly introduce the application named **Load Forecasting (LF)**, and then show how two different building datasets can be used for this application.
## Load Forecasting
The Load Forecasting can be used to predict the next timestamp load of a group of building systems by training a ML model with histrical electricity data of the related systems. As there are limited datasets are public for Cooling Load Forecasting, and both of these two task are predicting load for demandside equipments. Thus we use the Load Forecasting for showing cases here,
In general, a ML model construction process can be followed to get this model, which consists of data access, data processing, model training, model evaluation orderly.
## Public Building Datasets
Besides the EMSD data, we also provide an open-source dataset from project [**Genome**][genome].
## Model Introduction
### Model 1
Model 1 is a [Random Forest][RF] model which using the historical data from various systems of the building (e.g., chilled water system and hot water system) and solar illuminance data to train an ML model. Specifically, for the **Genome** datasets, the following sensing data are required:

+ **Chilled Water Flow**
+ **Hot Water Flow**
+ **Solar illuminance**

### Model 2
Model 2 is a [LSTM][LSTM] model which using the time-series data from both electrical and non-electrical systems and the weather data to train a neural network. This model require further data and the following data can serve it:

+ **Chilled Water Flow**
+ **Hot Water Flow**
+ **Solar Illuminance**
+ **Outdoor Temperature**
+ **Building Electricity**

## Example 1: Using Genome Data with Energon for Model 1
You may feel intractable at the first glance. Here, we provide a tool [**Energon**][energon] may assist you. The following steps can guide you go through the entire process.

### Step 1. Install the Energon tool and datasets
Firstly, click [here][download2] to download the Energon tool from google driver to local. Decompress the zip file and you find the dir structure looks like this:
```
Energon
│   README.md
│   energon_example.py  
│   model_training.py
│   model_evaluation.py
│ 
└───energon
│ 
└───Genome
│ 
└───Brick
│ 
└───ontology
```
The example codes are prepared in the **energon_example.py** file.


### Step 2. Writing EnergonQL to extract the data required for LF
By writing EnergonQL, [**Energon**][energon] can assist to access the **Genome** data. For example:

`SELECT Chilled_Water + Hot_Water + Solar`\
`FROM Building A`\
`WHERE A.id = 'Genome'`

This query extracts the above list of features in **Genome**

As these codes prepared in the **energon_example.py** file like this:
![image](https://github.com/fangger4396/energon_example/blob/main/img/screenshot2.png)
Run this file in your ternimal and you will get data as following screenshot shows:
![image](https://github.com/fangger4396/energon_example/blob/main/img/screenshot.png)
### Step 3. Train the model
After extracting the required data, you can process it and use it to train model just like any stardard ML model training process.
You can run the **model_training.py** to reproduce it.
By using these features as input of model 1, the accuracy of model 1 for **Genome** is 58% with the **percentage error** as metric.
If successful, you can see the parameters of the model like this:
![image](https://github.com/fangger4396/energon_example/blob/main/img/screenshot3.png)
## Example 2: Using Genome Data with Energon for Model 2

### Step 1. Install the Energon tool and datasets
As you have downloaded the Energon tools, you can start from step 2 here.

### Step 2. Writing EnergonQL to extract the data required for LF
You can write **EnergonQL** queries to extrac the followling list of features of **Genome** data for Model 2.

`SELECT Chilled_Water + Hot_Water + Solar + Electricity + Weather`\
`FROM Building A`\
`WHERE A.id = 'Genome'`

### Step 3.  Train and evaluate the model
After extracting the required data, you can process it and use it to train model just like any stardard ML model training process.
You can run the **model_training.py** to reproduce it.
By using these features as input of model 1, the accuracy of model 1 for **Genome** is 85% with the **percentage error** as metric.


## Example 3:Using EMSD Data with Energon for Model 1

`SELECT Chiller + Solar`
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
