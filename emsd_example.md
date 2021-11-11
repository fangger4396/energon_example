# Example for Cooling Load Forecasting
We provide a few examples on the general pipeline to develop an AI model for a cooling load forecasting problem. To avoid directly working on the problem of the AI Challenge, we choose the Genome data set and we choose to solve an electricity load forecasting problem. The general pipeline is the same and contains three steps:  
1.   Extract a subset of useful data for model training
2.   Apply an algorithm for model training
3.   Testing the model accuracy

## Model Introduction
Model we used here is a [LSTM][LSTM] model which using the time-series data from chiller system and the weather data to train a neural network. This model require  data and the following data can serve it:

+ **Flowrate of chiller plant**
+ **Temperature of chiller plant**
+ **Electricity power of chiller plant**

## Manual Way
Without loss of generality, we show how to extract the **flowrate** data of **chiller plant** manually here.

We firstly observe the EMSD data. Since each .csv file of EMSD data is the collection of data from a single sensor, we trace the flowrate data by listing all the files whose name contains *CP*(denotes Chiller Plant) and *FLOWRATE* (denotes flow rate).
![image](https://github.com/fangger4396/energon_example/blob/main/img/shot1.png)
Then we check files we found and locate the data we need. Here, **WKGO.CP-NT-CHWS-EM.FLOWRATEV.csv** and **WKGO.CP-NT-CHWS-EM.FLOWRATEV.csv** are what we need. Besides, for each file, only the column named *data* is valid values we need.
![image](https://github.com/fangger4396/energon_example/blob/main/img/shot3.png)
Finally, we merge the data we need by some scripts to generate a new .csv file. This another .csv file can be seen as the input of the above model training algorithm.

Note that only **flowrate** data were found so far. The same process should go for other features.
## Using Energon
If you feel the above method intractable at the first glance. Here, we provide a tool [**Energon**][energon] may assist you. The following steps can guide you to go through the entire process.

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
└───EMSD
  └───EMSDdatafiles
```
The example codes are prepared in the **data_extraction.py** file.
### step 2. Writing EnergonQL to extract the data required
By writing EnergonQL, [**Energon**][energon] can assist to access the **EMSD** data. For example:

`SELECT Chiller(A) * (FLOW_RATE(A) + Temperature(A) + Power(A))`\
`FROM Building A`\
`WHERE A.id = 'EMSD'`

This query extracts the above flowrate features of chillers in **EMSD**

As these codes prepared in the **data_extraction.py** file like this:
![image](https://github.com/fangger4396/energon_example/blob/main/img/screenshot2.png)
Run this file in your ternimal and you will get data as following screenshot shows:
![image](https://github.com/fangger4396/energon_example/blob/main/img/screenshot4.png)

## The following AI learning process
### Train the model
After extracting the required data, you can process it and use it to train model just like any stardard ML model training process.
You can run the **model_training.py** to reproduce it.

If successful, you can see the parameters of the model like this:
![image](https://github.com/fangger4396/energon_example/blob/main/img/screenshot3.png)

### Evaluate the model
  As the model trained, you can evaluate it by running the **model_testing.py** file. You can see by using these features as input of model 1, the accuracy of model 1 for **EMSD** is 58% with the **percentage error** as metric.

