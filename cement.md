# Examples on Load Forecasting Model Development
We provide a few examples on the general pipeline to develop an AI model for a load forecasting problem. To avoid directly working on the problem of the AI Challenge, we choose the Genome data set and we choose to solve an electricity load forecasting problem. The general pipeline is the same and contains three steps:  
1.   Extract a subset of useful data for model training
2.   Apply an algorithm for model training
3.   Testing the model accuracy
 
## Public Building Datasets
The open-source dataset from project **Genome** is publicated and detailed [here][genome].
## Model Introduction

### Model 1
Model 1 is a [LSTM][LSTM] model which using the time-series data from both electrical and non-electrical systems and the weather data to train a neural network. This model require  data and the following data can serve it:

+ **Chilled Water Flow**
+ **Hot Water Flow**
+ **Solar Illuminance**
+ **Outdoor Temperature**
+ **Building Electricity**

### Model 2
Model 2 is a [Random Forest][RF] model which using the historical data from various systems of the building (e.g., chilled water system and hot water system) and solar illuminance data to train an ML model. Specifically, for the **Genome** datasets, the following sensing data are required:

+ **Chilled Water Flow**
+ **Hot Water Flow**
+ **Solar illuminance**

## Example 1: Using Genome Data with Energon for Model 1
You may feel intractable at the first glance. Here, we provide a tool [**Energon**][energon] may assist you. The following steps can guide you go through the entire process.

### Step 1. Install the Energon tool and datasets
Firstly, click [here][download2] to download the Energon tool from google driver to local. Decompress the zip file and you find the dir structure looks like this:
```
Energon
├───README.md
├───data_extraction.py 
│
├───Model
│ ├───model_training.py
│ └───model_testing.py
│ 
└───Genome
  └───Genomedatafiles
```
The example codes are prepared in the **data_extraction.py** file.


### Step 2. Writing EnergonQL to extract the data required for LF
By writing EnergonQL, [**Energon**][energon] can assist to access the **Genome** data. For example:

`SELECT Chilled_Water + Hot_Water + Solar + Electricity + Weather`\
`FROM Building A`\
`WHERE A.id = 'Genome'`

This query extracts the above list of features in **Genome**

As these codes prepared in the **data_extraction.py** file like this:
![image](https://github.com/fangger4396/energon_example/blob/main/img/screenshot2.png)
Run this file in your ternimal and you will get data as following screenshot shows:
![image](https://github.com/fangger4396/energon_example/blob/main/img/screenshot.png)
### Step 3. Train the model
After extracting the required data, you can process it and use it to train model just like any stardard ML model training process.
You can run the **model_training.py** to reproduce it.

If successful, you can see the parameters of the model like this:
![image](https://github.com/fangger4396/energon_example/blob/main/img/screenshot3.png)

### Step 4. Evaluate the model
As the model trained, you can evaluate it by running the **model_testing.py** file. You can see by using these features as input of model 1, the accuracy of model 1 for **Genome** is 58% with the **percentage error** as metric.

## Example 2: Using Genome Data with Energon for Model 2

### Step 1. Install the Energon tool and datasets
As you have downloaded the Energon tools, you can start from step 2 here.

### Step 2. Writing EnergonQL to extract the data required for LF
You can write **EnergonQL** queries to extrac the followling list of features of **Genome** data for Model 2.

`SELECT Chilled_Water + Hot_Water + Solar`\
`FROM Building A`\
`WHERE A.id = 'Genome'`

The **Genome_query_2** in the **data_extraction.py** helps you to execute the query.

### Step 3.  Train and evaluate the model
After extracting the required data, you can process it and use it to train model just like any stardard ML model training process.
You can run the **model_training.py** to reproduce it.

### Step 4. Evaluate the model
Again, you can evaluate it by running the **model_testing.py** file. By using these features as input of model 2, the accuracy of model 1 for **Genome** is 85% with the **percentage error** as metric.


## Example 3 (bonus): Using EMSD Data with Energon for Model 1

We also provide partial data of EMSD for a slight attempt of data extraction. You can use the following EnergonQL query to extract data for Model 1.

`SELECT Chiller + Solar + Power`\
`FROM Building A`\
`WHERE A.id = 'EMSD`

By using these features as input of model 1, the accuracy of model 1 for **EMSD** is 71% with the **percentage error** as metric.


[genome]:https://github.com/buds-lab/the-building-data-genome-project
[brick]:https://brickschema.org/ontology/
[energon]:https://github.com/fangger4396/energon_example/blob/main/Energon.md
[download]:https://github.com/fangger4396/energon_example/blob/main/cement.md
[RF]:https://www.sciencedirect.com/science/article/pii/S0378778818311290
[LSTM]:https://www.sciencedirect.com/science/article/pii/S0306261917302921
[download2]:https://drive.google.com/file/d/19sGWnrKLrjlgX7xwI-b-a2QgN8AuFI6J/view?usp=sharing
