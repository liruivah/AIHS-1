# AIHS

## Overview

AIHS is an machine-learning-based self-healing prototype that provides automated intelligent healing for cloud-scale data centers. This source code showcases the complete workflow of AIHS and its usages.



## Prerequisite

AIHS is built in Python and requires the following dependencies:

+ Python3

+ Numpy, pandas

	+ ```python
		pip3 install numpy
		pip3 install pandas
		```

+ Sklearn, lightgbm

	+ ```python
		pip3 install sklearn
		pip3 install lightgbm
		```



## Source code

The source code include the following file and directories:

+ DataGenerator.py
	+ The script that generates the synthetic dataset for verifying the AIHS workflow
+ AIHS_Training.py
	+ The script that AIHS trains the machine learning models for the Mapper, Predictor, and Controller
+ AIHS_api.py
	+ The script that implement the three-stage workflow of AIHS
	+ Runing this script to find repair action for each given monitoring logs 
+ dataset
	+ The directory where a small synthetic dataset is provided
+ model
	+ The directory where the well-trained models is provided



## Examples

Following we show how to run the example we provided:

+ ```python
	### Step 1: generate the dataset
	python3 DataGenerator.py 
	# the synthetic records will be generated and overwrite the ./dataset/train.csv
	# modified the source code can change the number of records to generate
	# by defualt, the provided trace incldue 500 records
	# df=DG.gen_data(500,'./Dataset/train.csv')
	```

+ ```python
	### Step 2: train the model
	python3 AIHS_Training.py 
	# Trained the models for Mapper, Predictor, and Controller uisng the trace in ./Dataset
	# 
	# change the parameters for following functions to choose different models.
	# mapper=Mapper('LDA',df)
	# predictor=Predictor(df,mapper,'gbdt')
	# controller=Controller(mapper,df,'gbdt')
	# 
	# by defualt, we use LDA in the Mapper, GDBT in Predictor and Controller
	# Three well-trained model is put in ./model
	```

+ ```python
	### Step 3: simulate the self-healing workflow
	python3 AIHS_api.py 
	# Run the self-healing for the monitoring log example we given in the script
	# User can chagne to any other monitoring log to check the output 
	```

+ Sample output

	+ {'hostname': '12x8dj02', 'timestamp': 12345, 'action': ['RI']}
