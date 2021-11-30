## Example of extracting data from raw EMSD data
Here, we provide an example to show how to extract the data you can use to train the cooling load prediction model in the competition from the **raw EMSD data**. As we have stored the raw EMSD data in Energon, you should firtly download the Energon and install it for further use.
## The raw EMSD data
The raw EMSD data is different from what you recived from the organizers of the competition which can directly used for model training. The raw EMSD data is much more complex and coarse. Thus, we firstly give a full view of the raw EMSD data.

The raw EMSD data are collected by multiple sensors which distribute in different systems (e.g., Chillers, AHUs, Boilers, etc.) in the EMSD building and are varying in types (e.g., temperature, humidity, flow rate, etc.).

Without loss of generality, we show how to extract the **flowrate** data of **chiller plant** manually here.

We firstly observe the EMSD data. Since each .csv file of EMSD data is the collection of data from a single sensor, we trace the flowrate data by listing all the files whose name contains *CP*(denotes Chiller Plant) and *FLOWRATE* (denotes flow rate).
![image](https://github.com/fangger4396/energon_example/blob/main/img/shot1.png)
Then we check files we found and locate the data we need. Here, **WKGO.CP-NT-CHWS-EM.FLOWRATEV.csv** and **WKGO.CP-NT-CHWS-EM.FLOWRATEV.csv** are what we need. Besides, for each file, only the column named *data* is valid values we need.
![image](https://github.com/fangger4396/energon_example/blob/main/img/shot3.png)
Finally, we merge the data we need by some scripts to generate a new .csv file. This another .csv file can be seen as the input of the above model training algorithm.

Note that only **flowrate** data were found so far. The same process should go for other features.
## Installation of Energon
## Query data from raw EMSD data
