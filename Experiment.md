# Run Experiments and Train Models (25-30%)

## Create models by using Azure Machine Learning Designer
* create a training pipeline by using Azure Machine Learning designer
* ingest data in a designer pipeline
* use designer modules to define a pipeline data flow
* use custom code modules in designer

## Run training scripts in an Azure Machine Learning workspace
* create and run an experiment by using the Azure Machine Learning SDK
* configure run settings for a script
* consume data from a dataset in an experiment by using the Azure Machine Learning SDK

## Generate metrics from an experiment run
* log metrics from an experiment run
* retrieve and view experiment outputs
* use logs to troubleshoot experiment run errors

## Automate the model training process
* create a pipeline by using the SDK
* pass data between steps in a pipeline
* run a pipeline
* monitor pipeline runs

The **scikit-learn estimator** provides a simple way of launching an SKLearn training job on a compute target. It is implemented through the scikit-learn class, which can be used to support single-node CPU training.

Azure Machine Learning pipeline modules can validate, analyze, and transform your data to ensure your models are accurate. As you link pipeline modules, you control what data flows from one module to the next in your workflow.

**Select Columns in Dataset module** to identify the columns that should be processed and sent to the next pipeline element. By default, no columns are selected, and you will receive an error indicating that a value is required until you select at least one column.

The Select Columns in Dataset module supports several methods for identifying columns. You can select columns by name, type, or column index. As part of this process, you can define conditions that can filter your data based on type. For example, you could create a condition to exclude all string column types.

Select Column in Dataset is used to specify which columns are included in the next activity of the training pipeline. It will not allow you to remove rows that do not contain values.

**Clean Missing Data module**: You use the Clean Missing Data module to ensure that your data is as complete as possible prior to machine learning processing. When configuring this module, you need to specify the columns that contain missing values that you need to modify. You can configure the module to remove the entire row when the revenue column is empty. This keeps the rows in the original dataset, but the removed rows are not to be used in the model training.

A substitution value is an explicit value that is used to replace missing values. For example, you may replace missing values with a zero.

**SMOTE** is a statistical technique used to append number of cases to your dataset and ensure balance for the new samples created. This technique can be used to remove imbalance of a certain class in your dataset.

**Normalize Data module** is used to normalize columns within the dataset to eliminate bias that might be caused by large differences in the unit of values present in a column.You can normalize column values in such cases to fall between O and 1.

*Normalization* is a technique that is often applied as part of data preparation for machine learning. You would change the numeric data in the columns to use a common scale without distorting differences in the range of values or losing information.

Normalize Data allows you to configure all columns that contain numerical data to have the same scale without losing information. This will allow the training step to eliminate bias that could be associated with higher values because of certain column value units.

**Partition and Sample module**. This module helps create partition of the source dataset and maintain the same ratio of values. This is useful to reduce the size of the dataset and not eliminate imbalance of the source data. This module performs sampling on a dataset and 
analyzes the data without losing meaning.

**Split Data module**. The Split Data module is used to divide the dataset into two distinct sets based on the splitting mode provided. This is useful when training models by creating a training set and a testing set.

**Split Data module**. This module is used when you need to separate data into training and testing sets. You can customize the way data is divided. The module also provides options to randomize data selection.

**Join Data module**. This module is used to merge two datasets using a database-style join operation.

**Clip Values module**. This module allows you to replace data values that are above or below a specified threshold with a mean, a constant, or other substitute value.

**Inference cluster**. In order to host a real-time web service endpoint, you would have to create a cluster consisting of an Azure Kubernetes Service (AKS) instance or Azure Container Instance (ACI) managed by Azure. AKS is recommended for production use, while ACI is used primarily for small models or for development/testing purposes. This is the only type of cluster that is supported for deploying an 
inference pipeline as a hosted real-time service.

Compute instance, compute cluster, and attached compute are not supported to run inference pipelines as a real-time service. These clusters are more suited to host training and batch pipelines.

Specify a virtual network and ensure **head and worker nodes** can communicate with each other. Training video game machine learning models uses a process known as reinforcement learning (RL). RL machine learning agents take actions and then observe the results as a way of seeking rewards. Because RL is compute intense, it is typically performed across multiple compute nodes, known as head and worker nodes. In Azure Machine Learning, RL requires that you specify a virtual network that does not block the ports that nodes need to communicate.

You create a file dataset to reference the unstructured file or files you want to use in your machine learning experiments. In machine learning experiments, a FileDataset may be downloaded to compute targets or stored elsewhere and mounted to the experiment.

The **Estimator class** can be used when a predefined machine learning framework estimator does not already exist in Azure Machine Learning. For reinforcement learning, Azure Machine Learning provides the ReinforcementLearningEstimator class.

**SKLearn class** is used when running Scikit-learn training scripts. Scikit-learn is a Python-based machine learning library that only supports single-node compute targets.

When a new workspace is created, it contains a *default datastore*, **workspaceblobstore**. In order to retrieve the default datastore, you can use the **get_default_datastore** Workspace method. The workspaceblobstore datastore cannot be removed from the workspace.

You can also create a reference to workspaceblobstore using the datastore class. You can use the get method from the datastore class to retrieve a datastore by name. The following code retrieves a datastore named workspaceblobstore:

    my_datastore = Datastore.get(workspaceblobstore) 

**set_default_datastore method**: You can use this command to set a new default datastore.

All workspaces include an automatically registered blob container and file share. The file share - **workspacefilestore** - is used to store notebooks.

Azure Machine Learning allows you to track multiple metrics for your experiments. These metrics are stored in the experiment's **run record** for later retrieval and analysis, and the same metric can be logged within a run more than once. The run.log method can be used to log string or numerical scalar values and accepts three parameters, the metric name, the value to be logged, and an optional description.

The Experiment.submit method can be configured with the show_output parameter to enable local logging during the training process.

The Experiment.start_logging() enables logging for run-related data within the experiment. This will not show the logs generated during the training process.

The ComputeTarget.wait_for_completion method configures logging during a compute target creation. This will not show the logs generated during the training process.

The services.get_logs() enables logs to be retrieved for a previously deployed web service. The logs may contain detailed information about a past run, but they do not show the logs generated during the training process.

You plan to configure logging for an experiment that explores data associated with gender distribution within organizations across the world. The experiment must draw a box plot of genders by country. You need to use the appropriate logging method to render the plot for the experiment run object.
**log_image()** This method logs a .PNG image file or a matplotlib plot to the run. These images will be visible and comparable in the run record.

**log_table()** This method can be used to log a dictionary object to the run with the given name. This method will not render a plot.
**log()** This method is used to log a numerical or a string value to the run with a given name. This method will not render a plot.
**log_list()** This method is used to log a list of values to the run with a given name. This method will not render a plot.
**log_row()** This method creates a metric with multiple columns. Each named parameter generates a column with the value specified. This method will not render a plot.

**get_file_names()** function. This function will list all the files that are associated with the experiment run object. 
**get_status()** function is used to fetch the status of the last run.
**get_details_with_logs()** This function is used to get the status of the last run, along with log file contents. 
**get_details()** This function is used to get the definition, status information, current log files, and other details of the run.

Automated machine learning requires that input data be stored in tabular form. You create a tabular dataset to reference tabular data, such as that found in a comma-separated-value (CSV) file. You use the Dataset.Tabular.from_delimited_files method to register tabular data in a dataset.

When configuring a pipeline using Azure Machine Learning SDK, you can define automated machine learning settings that control how the experiment is run. These settings are typically defined in dictionary format and passed to the AutoMLConfig class. If the featurization parameter is set to auto, input data will automatically be preprocessed and missing values will be handled.

Machine learning pipelines require remote compute and cannot be run on a local compute target. Remote compute targets can reside inside or outside of the Azure cloud.

Azure Machine Learning supports several locations for storing experiment output. Files can be saved to storage on the local compute instance; however, these files do not persist across training runs. To store files for later analysis and review, you should use an Azure Machine Learning datastore, or you should write to the ./outputs or ./logs folders. Files written to the ./logs folder are uploaded in real time.

You should not create a FileDataset. You create a file dataset to reference the unstructured file or files you want to use in your machine learning experiments.

Azure Machine Learning pipelines are workflows that represent a series of machine learning tasks. Pipeline tasks can be executed independently from the underlying data, and you can register new datasets for each pipeline run, if necessary.

You can allow other users to run the pipeline using custom inputs by publishing the pipeline. To do this, you must first create a pipeline parameter object using the PipelineParameter class, which allows you to specify the default value of the pipeline parameter. Once this is complete, you can add your PipelineParameter to any step, including script steps, when constructing a pipeline. 

Finally, you can use the publish_pipeline method to publish the pipeline. This creates a REST endpoint that can by accessed by external users. 

You should not save the pipeline to a YAML file. You use this option to export the pipeline steps and then import them into another system.

You can use the OpenCensus Python library to forward Azure Machine Learning logs to Application Insights to provide advanced pipeline monitoring, tracing, and metrics tracking. To do this, you define a Custom Dimensions dictionary which provides field names for your logging data. These fields can then be specified 
in Application Insight queries.

**run_type** field to differentiate between training and scoring runs. In machine learning, you train a model by applying an algorithm to input data. Scoring is the process of using a trained model to predict future values.
**step_id** field to focus on a specific issue. This allows you to view details for a specific step. For example, you could query the logs for all entries with the same step_id.
**parent_run_id** field to view logs for all steps over time. Pipelines are machine learning workflows composed of individual steps. By querying the parent_run_id, you can view information for all steps that are part of a run.

The basic structure of a SQL query includes SELECT and FROM clauses. 

The **SELECT** clause allows you to specify the data you want, and a simple query usually consists of one or more table columns. 

The **FROM** clause allows you to specify the database tables that hold the data you need. When using the Apply SQL Transformation module, datasets are represented as tl, t2, or t3.

If you are combining data from two datasets, you include the name of the first dataset in the **FROM** clause, and then use the **JOIN** clause to specify the second dataset. 

The **ON** clause identifies *the column that the two datasets have in common*, in this case, the departmentlD.

The **GROUP BY** clause tells the module how to group data prior to applying the group function, in this case, the average function.

The Execute Python Script module can be added to a drag-and-drop designer pipeline to run Python code. This is useful in cases where an existing Azure Machine Learning designer module does not provide the functionality you need for your experiments. The Execute Python Script module requires that your script uses an entry-point function named **azureml_main**

You can use the Azure Machine Learning SDK to create and manage machine learning workspaces, create and manage experiments, load data, and train machine learning models. If you want to use Azure Machine Learning Studio to view associated experiment graphs or individual runs, you can **call the experiment variable** to generate an Azure Machine Learning Studio link. Following this link takes you to the Azure Machine Learning studio page for your experiment. 

The **run.complete** method is called after each iteration of an experiment. As the name indicates, this method marks the run as completed. 

The **run.upload_file** method is used to serialize and upload the model to Azure Machine Learning Studio. You can then use Azure Machine Learning SDK to download the run at a future date. 

**experiment.start_logging** method is used to initiate an interactive logging session for an experiment. 

Azure Machine Learning allows you to track multiple metrics for your experiments. These metrics are stored in the experiment's run record for later retrieval and analysis, and the same metric can be logged within a run more than once. The **run.log** method can be used to log string or numerical scalar values and accepts three parameters, the metric name, the value to be logged, and an optional description. 

**run.log_list** method allows you to log lists of values in an experiment run. A value list is comparable to a one-dimensional array. 

You can use the **run.log_table** method to log a dictionary object to the run. A dictionary is sometimes referred to as an array and allows you to store key values along with associated data. 

The **run.tag** method allows you to tag a run with a string key. The value is optional. 

Drag the **Execute Python Script** module onto the designer canvas. This module can be added to a drag-and-drop designer pipeline to run Python code. This is useful in cases where an existing Azure Machine Learning designer module does not provide the functionality you need for your experiments. 

The **run.log_table** method to the code editor. Azure Machine Learning allows you to track multiple metrics for your experiments. These metrics are stored in the experiment's run record for later retrieval and analysis. You can use the run.log_table method to log a dictionary object to the run. A dictionary is sometimes referred to as an array, and it allows you to store key values along with associated data. 

The **run.start_logging** method is used for interactive runs, such as those executed from a Jupyter notebook. This method logs metrics to the experiment's run record. 

The **ScriptRunConfig** class is used to create an object that contains both training environment configuration information as well as a training script. This ScriptRunConfig object can be used to initiate a fully configured training run as part of a machine learning experiment. 

Azure Machine Learning supports several locations for storing experiment output. Files can be saved to storage on the local compute instance, but these files do not persist across training runs. To store files for later analysis and review, you should use an Azure Machine Learning datastore, or you should write to the outputs or logs folders. *Files written to the ./logs folder are uploaded in real time*.

*Files written to the outputs folder persist across experiments, but they are not uploaded in real time*.

The **run.log("experiment_output",O)** method can be used to log scalar string or numerical values. This method does not upload output files. 

The **run.get_file_names()** method is used to list all files that have been stored by the training run. 

You should perform the following steps in order: 
1. Register a new Azure Storage file container datastore. 
2. Create a PipelineData object. Specify a name and output datastore. 
3. Specify a PipelineData object for data output. 
A PipelineData object can be used to pass data between steps in a pipeline. When you create a 
PipelineData object, you must specify a name. If you do not provide a data store reference, the default 
workspace datastore will be used. In this scenario, you are required to use a named datastore, so the first 
action requires registering a new file container datastore. 
Once a PipelineData object has been created, you can specify the output of a pipeline step to be written to 
this object in the same way as you would to a local folder. In successive pipeline steps, you can then read 
data by referencing the PipelineData object created in an earlier step. 
You should not retrieve the default datastore from the current workspace. You can use the get() method to 
retrieve a datastore by name. The following code retrieves a datastore named default-datastore: 
my_datastore = Datastore.get(default-datastore) 
You should not register a new dataset version for each pipeline pass. Azure Machine Learning allows you to 
register a new dataset using an existing dataset name using versioning. A version is a bookmark of the data's 
state and is useful in cases where new data needs to be used for retraining. By creating versions, you can 
return to a specific version of the dataset if necessary. 

You should perform the following actions in order: 
1. Define a PipelineParameter object. 
2. Specify a default pipeline parameter value. 
3. Add the PipelineParameter object as a script argument. 
4. Use the publish_pipeline method to publish the pipeline. 
Azure Machine Learning pipelines are workflows that represent a series of machine learning tasks. Pipeline 
tasks can be executed independently from the underlying data, and you can register new datasets for each 
pipeline run, if necessary. 
You can allow other users to run the pipeline using custom inputs by publishing the pipeline. To do this, you 
must first create a pipeline parameter object using the PipelineParameter class, which allows you to specify 
the default value of the pipeline parameter. Once this is complete, you can add your PipelineParameter to 
any step, including script steps, when constructing a pipeline. Finally, you can use the publish_pipeline 
method to publish the pipeline. This creates a REST endpoint that can by accessed by external users. 
You should not save the pipeline to a YAML file. You use this option to export the pipeline steps and then 
import them into another system. 

