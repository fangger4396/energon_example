### Example for Cooling Load Forecasting
We provide a few examples on the general pipeline to develop an AI model for a cooling load forecasting problem. To avoid directly working on the problem of the AI Challenge, we choose the Genome data set and we choose to solve an electricity load forecasting problem. The general pipeline is the same and contains three steps:  
1.   Extract a subset of useful data for model training
2.   Apply an algorithm for model training
3.   Testing the model accuracy

### Model Introduction
Model we used here is a [LSTM][LSTM] model which using the time-series data from chiller system and the weather data to train a neural network. This model require  data and the following data can serve it:

+ **Flowrate of chiller plant**
+ **Temperature of chiller plant**
+ **Electricity power of chiller plant**
+ **Outdoor Temperature**

### Manual Way
Without loss of generality, we show how to extract the **flowrate** data of **chiller plant** manually here.

We firstly observe the EMSD data. Since each .csv file of EMSD data is the collection of data from a single sensor, we trace the flowrate data by listing all the files whose name contains *CP*(denotes Chiller Plant) and *FLOWRATE* (denotes flow rate).
![image](https://github.com/fangger4396/energon_example/blob/main/img/shot1.png)
Then we check files we found and locate the data we need. Here, **WKGO.CP-NT-CHWS-EM.FLOWRATEV.csv** and **WKGO.CP-NT-CHWS-EM.FLOWRATEV.csv** are what we need. Besides, for each file, only the column named *data* is valid values we need.
![image](https://github.com/fangger4396/energon_example/blob/main/img/shot2.png)
Finally, we merge the data we need by some scripts to generate a new .csv file. This another .csv file can be seen as the input of the above model training algorithm.

Note that only **flowrate** data were found so far. The same process should go for other features.
### Using Energon

### Model training

### Model testing
