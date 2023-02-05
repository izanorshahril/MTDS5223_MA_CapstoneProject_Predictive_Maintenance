# MTDS MA Capstone Project Report: Predictive Maintenance

[comment]: # (This document is intended to capture the use case summary for this engagement. An executive summary should contain a brief overview of the project, but not every detail. Only the current summary should be captured here and this should be edited over time to reflect the latest details.)
[comment]: # (Some ideas of what to include in the executive summary are detailed below. Please edit and capture the relevant information within each section)
[comment]: # (To capture more detail in the scoping phase, the optional template Scoping.md may be utilized. If more detail around the data, use case, architecture, or other aspects needs to be captured, additional markdown files can be referenced and placed into the Docs folder)

This repository is for MTDS5223 Manufacturing Analytics Capstone Project titled Predictive Maintenance.

Team members: 
Iza Norshahril Bin Ibrahim M032110060,
Ang Siew Fen M032110048,
Goh Chau Fong M032110046

### Problem Background
Overall Equipment Effectiveness (OEE) is a kind of standard that to measure manufacturing productivity performance. OEE measurement can be help in underlying the losses and gain important insight on improve the current manufacturing process. OEE is measuring by 3 main factors which are availability (equipment planned & unplanned stop), performance (any slow cycle or small stoppage) and quality (yield).
Below show the OEE performance based on Molding machine in our case study:
![image](https://user-images.githubusercontent.com/124276426/216356722-50d89466-39d5-413b-aa71-5c404030bb05.png)


#### Ishikawa Diagram
Below show the Ishikiwa Diagram for this projectv which finding the root cause contribute to OEE deterioration in machine.
We are focus on 5M in this case, which are Man, Machine, Material, Method and Milieu (which meaning is environment):
![image](https://user-images.githubusercontent.com/124276426/216355247-c0addf7a-b2c1-4183-a5ca-242a09363e12.png)

#### Problem Selection
Below are the problem selection list, where from this list we observe that in 5M's machine and man having high impact to our OEE, where late response and high stoppages in machine will cause OEE deterioration
![image](https://user-images.githubusercontent.com/124276426/216357025-e8ca8ed6-3c3f-4b25-981e-64d7216fc2b6.png)

Problem Selection Matrix showing the criticality, severity and ranking for our target problem selection
![image](https://user-images.githubusercontent.com/124276426/216357728-a9f2cdef-64c8-4e19-bbd5-58eaad8c6645.png)


### Problem Statement
Equipment in manufacturing can contributes to the OEE factors (available, performance, quality) if not well maintained. Equipment without being repaired before it fails, can directly or indirectly causing further damage to the equipment and connected systems. In order to secure quality and cost saving, it is crucial to reduce any unscheduled machine breakdown. Preventive maintenance was most common technique that implemented in manufacturing sector these year. However, with preventive maintenance, the limitation was only periodic scheduling to perform health check and service to machine. In proactive manner, predictive maintenance can use to predict the failure, and before machine part breakdown, it take to precaution to repair or change part to reduce sudden failure during production running which causing un-scheduled downtime. Most of predictive maintenance today align with the implementation of Industry 4.0 is using edge platform attached to the machine by using sensor data as input that detect signal abnormality and critical threshold but there are still many legacy machines that not ready to be modernized with such capability.

### Objective
Our objective in this project is:-
1) To predict event which can cause unscheduled downtime for the running equipment
2) To develop a proof-of-concept (POC) prediction model based on machine alarm and status data
3) To evaluate model performance


### Predictive maintenance
Predictive maintenance is a proactive approach to maintenance that uses data, analytics and machine learning algorithms to predict when equipment is likely to fail and schedule maintenance accordingly.

#### PM vs PdM
Predictive maintenance and preventive maintenance are two types of maintenance strategies that are used to keep equipment functioning properly and extend its lifespan. While both strategies aim to reduce equipment downtime and improve reliability, there are some key differences between the two approaches:
##### Timing: Preventive maintenance is scheduled based on a predetermined schedule, such as a set number of hours of operation or calendar time. Predictive maintenance, on the other hand, is scheduled based on predictions made by machine learning models that analyze equipment data, such as temperature, vibration, and pressure.
##### Proactive vs. Reactive: Preventive maintenance is a proactive approach to maintenance, as maintenance activities are performed before failures occur. Predictive maintenance is a reactive approach, as maintenance is performed only when a failure is predicted.
##### Cost: Preventive maintenance can be more expensive as maintenance activities are performed regularly, regardless of the actual condition of the equipment. Predictive maintenance can be more cost-effective, as maintenance activities are performed only when necessary, reducing the overall maintenance cost.
##### Equipment Downtime: Preventive maintenance can result in unplanned downtime, as maintenance activities may be performed even when equipment is functioning properly. Predictive maintenance can reduce unplanned downtime, as maintenance is performed only when a failure is predicted.
![image](https://user-images.githubusercontent.com/124276426/216359179-851d8a67-1e23-456d-822c-226ee7f7270f.png)

## Methodology
We integrated basic Team Data Science Process (TDSP) Lifecycle  into DMAIC for methodology in our project. Data Science Lifecycle (DSLC) is list of steps in solving data-related problem using scientific and mathematical methods. TDSP Lifecycle is a team approach on DSLC projects. DMAIC is acronym for Define, Measure, Analyse, Improve and Control which is Six Sigma methodology for problem solving and improvement.


#### POC Architecture
![image](https://user-images.githubusercontent.com/124276426/216359369-3b877e1a-5737-42ed-b176-c3be4e41016f.png)

### Data EDA
This project is executed by three members. The project execute the various data science steps, creates and compares models, and deployes the final model using Rapid Miner. In this project, we involve collaboration software includes PowerBI, Python, Excel, and Rapid Miner.

### Metrics
Performance of the machine learning models will be evaluated on the test set of the machine alarm joined with the machine status dataset. Accuracy is measured and reported using AUC. AUC of > 0.8 will be considered acceptable and suitable for deployment.

#### ROI
For ROI, we are expecting to calculate the reduction of unscheduled downtime maintenance with implementation of prediction model versus existing unscheduled downtime. Due to the alarm data after maintenance didn’t analyse, unable to calculate the reduction of alarm detection / stoppage in equipment.

Based on unscheduled downtime data, it is around 1% of overall equipment time and equivalate to 50K USD of process cost. Estimate at least 50% of unscheduled downtime reduction with 25K gain through prediction model. 

## 2. Data Acquisition and Understanding

### Raw Data
Raw data are as shown as below:
![image](https://user-images.githubusercontent.com/124276426/216371229-e26ebcef-235c-4a4e-a60d-477d092ae476.png)
There are 2 data we are focus on:
1) Machine alarm data
2) Machine status data

![image](https://user-images.githubusercontent.com/124276426/216381512-6d5b83e4-869f-47c2-bf7b-54edf39c5dd3.png)

In previous literature review, it is observed that many research using combination of alarm and sensor data to perform the PdM. However due to lacking such of resource data, we decided to explore solely on alarm data and machine status data to check what is the result on the PdM modelling.

There are total 5 machines data is used where same equipment platform machine data is extracted. They are come from molding in assembly process. 
The machine status UDR (unschedule downtime for repair) is focus in this project. Besides, machine alarm collected period are from Jan2022 to Dec2022.

The raw data can be view in folder or link here:
https://github.com/izanorshahril/MTDS5223_MA_CapstoneProject_Predictive_Maintenance/blob/main/raw/machine%20status.xlsx
https://github.com/izanorshahril/MTDS5223_MA_CapstoneProject_Predictive_Maintenance/blob/main/raw/machine%20status.xlsx

This data was extracted from software which direct communicate and store machine alarm. For machine status, it is extracted from manufacturing Execution System (MES). 

There are a total of 52294 of rows for machine alarm and 191335 of rows for machine status.

Machine alarm contains various alarms timestamped to Machine A, B, C, D and E. Meanwhile, machine status contains the same machine status over the same period.

TARGET: Major Downtime (Yes/No)

FEATURES: Alarms

### Data Exploration
Data exploration is performed using the Python 3

![image](https://user-images.githubusercontent.com/124276426/216376181-8489aae7-663b-452f-ad33-27978a5d71a8.png)

Machine alarm data trend show that the alarm count is increasing over time, where in OEE is showed the OEE also decline over time,

![image](https://user-images.githubusercontent.com/124276426/216377425-c165d181-fba1-4351-98d2-4391d4c5cb84.png)

Where the distribution of alarm for 5 machines are consider equally, it is said to be the data are even for each machine, where we can generalize the alarm data without equipment info train into the model.

![image](https://user-images.githubusercontent.com/124276426/216377553-9c64aeb1-6123-48f8-bcb4-8ec20d01da98.png)

From data exploration, we also could have a glance on which are the top alarm in machine. However, our target for this project is to predict the major downtime and it caused by which attribute. Later we could compare to this Pareto chart whether top alarm causing the UDT in machine.

Next, by using Python, we could explore to descriptive statistic of our dataset, below show the statistic overview for our dataset:

![image](https://user-images.githubusercontent.com/124276426/216381122-255aa843-0ac7-42b9-bf1e-dffcc2d8ca06.png)

## 3. [**Modeling**](https://github.com/Azure/MachineLearningSamples-TDSPUCIAdultIncome/tree/master/code/02_modeling)

### Feature Engineering
For data engineering and preparation, we are follow the flow as below:

![image](https://user-images.githubusercontent.com/124276426/216382366-666586c8-9b62-46eb-b753-fd218ee3ba4a.png)

**Data cleanup: Removing columns and rows**
Prior to feature engineering, we removed columns with unknown values

![image](https://user-images.githubusercontent.com/124276426/216383174-711b7b93-c0a9-4926-9da8-823d31f69e03.png)

### Modeling training
We created several models with Rapid Miner. By testing out several dataset, which include raw dataset, normalized dataset, squared normalized dataset, & log dataset, we managed to result the table as below:
![image](https://user-images.githubusercontent.com/124276426/216816196-40353cc5-33e7-4740-82de-299a82d9a9fb.png)

While using different dataset, different features selection are manipulated to analyse which are the most suitable model to be perform PdM in case study. 

a = average alarm count

c = alarm count data

d = alarm clearing duration

s = machine UDR status statistic for each day

a & c & d & s = merged dataset of all above attribute

### Model evaluation
Accuracy of the models were measured using AUC on the test data set. AUC of both Elastic Net and Random Forest models were > 0.85. We save both models in pickled.pkl files, and output the ROC plots for both models. AUC of Random Forest model was 0.92 and that of the Elastic Net model was 0.90. In addition, for model interpretation, feature importance for the Random Forest model are output in a .csv file and plotted in a pdf (top 20 predictive features only). 


## 4. Result and Discussion

Based on 37603 models ran on normalized data, we observed below results:
![image](https://user-images.githubusercontent.com/124276426/216816033-28e93073-1453-4c6b-82b6-ffcd3801daed.png)

Most common models for predictive maintenance based on most early study is tree model such as Random Forest and Decision Tree, but we found that the result can be inconsistent prone to high classification error and is a bit lower than others. 

Gradient Boosted Tree is expected to has higher performance as it’s more complex and robust model based on multiple decision trees. 

Many industry experts also prefer Support Vector Machine (SVM) in predictive maintenance when we have high-dimensional data, well-suited if we have continuous data such as sensor log but from our result also it shows that SVM is also good in classification if we can make more features for it.

Naïve Bayes is expected to have lower performance result due to limitation of relationship between features which is hard to interpret in real-world situation.​

Logistic Regression and Fast Large Margin is good for binary classification, but we had lower result may be due to the quality of the data and available features for it.

Deep Learning unexpectedly has poorer data amongst the other models. This may be due to lack of labelled data, as deep learning need a large amount of data to be trained effectively. Other reasons are imbalanced data distribution which is typical in manufacturing, which is controlled to has very low fault occurrence plus the relationship between features and target variable also are not straightforward.

We found that Generalized Linear Model (GLM) has very good result. Fundamentally GLM is good when we have alarm data and historical machine with its target variable so GLM will learn the relationship between the alarm and the target make prediction. GLM also more robust and general and may be best for our limited feature dataset.


### Prediction
There are 2 part of prediction:


#### Result for T0 Down Time
Predict Major Down Time using Generalized Linear Model:

![image](https://user-images.githubusercontent.com/124276426/216815908-77e7afa0-3e59-4dcd-97ff-5005ac8e378e.png)

Confusion Matrix comparing different features selection:

![image](https://user-images.githubusercontent.com/124276426/216815951-0a613cd5-0c80-4607-8690-876d29d46b4f.png)


#### Result for T-1 Down Time 
Predicting day before Major Down Time using Generalized Linear Model:
P![image](https://user-images.githubusercontent.com/124276426/216815800-1ad2dd5e-3620-4adb-94fa-e347e69df8fe.png)

#### Confusion Matrix Comparison

By comparing
![image](https://user-images.githubusercontent.com/124276426/216815860-f297d567-87b8-4df0-b7f1-145061e307fb.png)


### Tools
Below are the tools that we utilized to perform analysis and prediction during this project:
![image](https://user-images.githubusercontent.com/124276426/216815755-25e299eb-6468-41d3-b8bf-87d0efaa50f1.png)


### Limitation
- Due  to limited data provisioning, data is limited to only for alarm and status. 
- No categorization on alarm for which module and its critical alarm. Difficulties to try other platform and tools (Azure, tensor, error troubleshooting, etc).
- Unable to try different model such as LSTM. 
- Team's technical knowledge constraint on predictive maintenance know-how.

### ROI Analysis
For ROI, we are expecting to calculate the reduction of unscheduled downtime maintenance with implementation of prediction model versus existing unscheduled downtime. Due to the alarm data after maintenance didn’t analyse, unable to calculate the reduction of alarm detection / stoppage in equipment. Based on unscheduled downtime data, it is around 1% of overall equipment time and equivalate to 50K USD of process cost. Estimate at least 50% of unscheduled downtime reduction with 25K gain through prediction model. 

## Architecture, Environments, Code Execution

#### Development
An [Azure Data Science Virtual Machine (DSVM) Windows Server 2016](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.windows-data-science-vm), (VM Size: [DS3_V2](https://docs.microsoft.com/azure/virtual-machines/windows/sizes), with 4 virtual CPUs and 14-Gb RAM). Although tested on an Azure DSVM.

We used the TDSP template in Azure Machine Learning to create a new project, and all code and documents were developed in this project. Instructions on how to create a new project in TDSP format is provided [here](https://github.com/amlsamples/tdsp/blob/master/Docs/how-to-use-tdsp-in-azure-ml.md).

Code is executed in the AMLW Python 3.5 environment using the Azure Machine Learning CLI. See Azure Machine Learning product documentation for information on installation and execution. Details about code and its execution are provided in the respective folders and subfolders under \Code.

Outputs generated from data preparation and modeling stages are stored in the root .\output folder. 

The deployment progress can be tracked with kubernetes from localhost:

<img src="./images/kubernetes.png">

## Version Control Repository
An empty Git repository is needed to version control contents of this project. 

#### Deployment
For deployment, we copied the following files in the project root directory:
1. Json file for input data format
2. The pickled Random Forest model file (CVRandomForesstModel.pkl) 
3. The scoring script, score.py, from the .\code\deployment folder

Service is run in the Azure Container Service (ACS). The operationalization environment provisions Docker and Kubernetes in the cluster to manage the web service deployment.

#### Code Execution
In this example, we execute code in **local compute environment** only. Refer to Azure Machine Learning documents for execution details and further options.

Executing a Python script in a local Python runtime is easy:

    az ml experiment submit -c local my_script.py

IPython notebook files can be double-clicked from the project structure on the left of the Azure Machine Learning UI and run in the Jypyter Notebook Server.

## Conclusion
Based on result matrix, Generalized Linear Model, Gradient Boosted Trees, and Support Vector Machine show better result compared to others aligned some of the research studies. We can have more options if we have more data such as sensor data and PM record. For the best model, we pick Generalized Linear Model due to good and consistent result when used with various datasets.Aggregation data as features is important, as from the performance matrix, aggregation alone can achieve fair result (>80% accuracy) compared to just using raw base data (~73%). Predicting a day before major down time has low accuracy because the time group is too large which is per 24 hours. We may accompany with multiple models to predict based on lesser time frame for better accuracy. Lastly, we may have better insight if we can analyze alarms on post downtime and maintenance.

[comment]: # (If there is a substantial change in the customer's business workflow, make a before/after diagram showing the data flow.)

### References
De Ron, A. J., & Rooda, J. E. (2005). Equipment effectiveness: OEE revisited. IEEE transactions on semiconductor manufacturing, 18(1), 190-196.​

Prasetyo, Y. T., & Veroya, F. C. (2020, April). An Application of Overall Equipment Effectiveness (OEE) for Minimizing the Bottleneck Process in Semiconductor Industry. In 2020 IEEE 7th International Conference on Industrial Engineering and Applications (ICIEA) (pp. 345-349). IEEE.​

Lopena, S., Bertumen, E., & Mondero, J. (2021). Integrated Capacity Planning Tool Implementation in an OSAT Company using the Six Sigma DMAIC Framework. In DLSU Research Congress 2021 (Vol. 6).​

Fischer, D., Moder, P., & Ehm, H. (2021, March). Investigation of predictive maintenance for semiconductor manufacturing and its impacts on the supply chain. In 2021 22nd IEEE International Conference on Industrial Technology (ICIT) (Vol. 1, pp. 1409-1416). IEEE.​

Chazhoor, A., Mounika, Y., Sarobin, M. V. R., Sanjana, M. V., & Yasashvini, R. (2020, October). Predictive maintenance using machine learning based classification models. In IOP Conference Series: Materials Science and Engineering (Vol. 954, No. 1, p. 012001). IOP Publishing.​

Zhang, M., & Wang, D. (2019). Machine Learning Based Alarm Analysis and Failure Forecast in Optical Networks. 2019 24th OptoElectronics and Communications Conference (OECC) and 2019 International Conference on Photonics in Switching and Computing (PSC).​

Butte, S., Prashanth, A.R. and Patil, S., 2018, April. Machine learning based predictive maintenance strategy: a super learning approach with deep neural networks. In 2018 IEEE Workshop on Microelectronics and Electron Devices (WMED) (pp. 1-5). IEEE.​

Van Staden, H. E., Deprez, L., & Boute, R. N. (2022). A dynamic “predict, then optimize” preventive maintenance approach using operational intervention data. European Journal of Operational Research, 302(3), 1079-1096.​

Jang, J., Nana, D., Hochschild, J., & de Lorenzo, J. V. H. (2021). Predicting Breakdown Risk Based on Historical Maintenance Data for Air Force Ground Vehicles. arXiv preprint arXiv:2112.13922.​

Susto, Gian Antonio; Schirru, Andrea; Pampuri, Simone; McLoone, Sean; Beghi, Alessandro (2015). Machine Learning for Predictive Maintenance: A Multiple Classifier Approach. IEEE Transactions on Industrial Informatics, 11(3), 812–820. doi:10.1109/tii.2014.2349359 

[Project Repository in GitHub](https://github.com/Azure/MachineLearningSamples-TDSPUCIAdultIncome)

[TDSP project template for Azure Machine Learning](https://aka.ms/tdspamlgithubrepo)
