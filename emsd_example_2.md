## Example of extracting data from raw EMSD data
Here, we provide an example to show how to extract the data you can use to train the cooling load prediction model in the competition from the **raw EMSD data**. As we have stored the raw EMSD data in Energon, you should firtly download the Energon and install it for further use.

## Installation of Energon
You can download the Energon [here][download2] to download the Energon tool from google driver to local. Decompress the zip file and you find the dir structure looks like this:
```
Energon
├───README.md
├───requirements.txt
├───data_extraction.py 
└───EMSD
  └───EMSD_data_files
```
The dependency of the Energon project is in the requirements.txt.

All the raw EMSD data are stored in the directory **EMSD**. Each csv file stores the data collected by a single sensor. Note that we only place a piece of data for these sensors (the data of 1st Jan. 2021) for this tutorial.

## The raw EMSD data
The raw EMSD data is different from what you recived from the organizers of the competition which can directly used for model training. The raw EMSD data is much more complex and coarse. Thus, we firstly try to give a summarize of the raw EMSD data.

The raw EMSD data are collected by multiple sensors which distribute in different systems (e.g., chillers, AHUs, boilers, etc.) in the EMSD building and are varying in types (e.g., temperature, humidity, flow rate, etc.). The EMSD building located in 1 Hoi Ting Road, Yau Ma Tei, Kowloon, Hong Kong. It consists of two office towers and has a total area of 98,000 m^2.

Without loss of generality, we show how to extract the **temperature** data of **chiller plant** manually here.

We firstly observe the EMSD data. Since each .csv file of EMSD data is the collection of data from a single sensor, we trace the flowrate data by listing all the files whose name contains *CP*(denotes Chiller Plant) and *TEMP* (denotes temperature) (highlight in yellow).
![image](https://github.com/fangger4396/energon_example/blob/main/img/emsd.png)
Then we check files we found and locate the data we need (highlight in red and green). Here, **WKGO.CP.NT.CHWR.TEMP.V.csv** and **WKGO.CP.NT.CHWS.TEMP.V.csv** are what we need. Besides, only the column named *data* is valid values we need.
Finally, we merge the data we need by some scripts to generate a new .csv file. This another .csv file can be seen as the input of the above model training algorithm.

Note that only **temperature** data were found so far. The same process should go for other features.

## Query data from raw EMSD data by Energon
Here, we simply give an example of writing query with Energon to query data from the raw EMSD data. You can easily recur it by running the **data_extraction** script.

By writing EnergonQL, [**Energon**][energon] can assist to access the **EMSD** data. For example:

`SELECT Chiller(A) * (FLOW_RATE(A) + Temperature(A))`\
`FROM Building A`\
`WHERE A.id = 'EMSD'`

This query extracts the above flowrate features of chillers in **EMSD** as follows:
![image](https://github.com/fangger4396/energon_example/blob/main/img/emsd2.png)

For further introduction of Energon, you can refer to [here][energon].


[genome]:https://github.com/buds-lab/the-building-data-genome-project
[brick]:https://brickschema.org/ontology/
[energon]:https://github.com/fangger4396/energon_example/blob/main/Energon.md
[download]:https://github.com/fangger4396/energon_example/blob/main/cement.md
[RF]:https://www.sciencedirect.com/science/article/pii/S0378778818311290
[LSTM]:https://www.sciencedirect.com/science/article/pii/S0306261917302921
[download2]:https://drive.google.com/file/d/19sGWnrKLrjlgX7xwI-b-a2QgN8AuFI6J/view?usp=sharing
