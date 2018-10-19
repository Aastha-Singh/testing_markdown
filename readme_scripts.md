### create_package.sh

This script automatically creates package to be used to train model either on local or on cloud.

#### Arguments:
```
* package_name: Provide name of the package
* config_file: Provide name of the configuration file to used to train the model
* utils_file: Provide name of the configuration file to used to train the model
* main_file: Provide name of the configuration file to used to train the model
* model_file: Provide name of the configuration file to used to train the model
* cloud: This will be "True" if package is to be used on cloud, otherwise "False"
```




### train_cloulml.sh


This script train model on Google Cloud ML.

#### Arguments:
```
* job: It is optional to give job name else it will take default name
* stream-logs: Block until job completion and stream the logs while the job runs
* runtime-version: Google Cloud ML Engine runtime version for this job
* staging-bucket: Bucket in which to stage training archives
* module-name: Name of the module to run
* packages: Path to Python archives used for training
* region: Region of the machine learning training job to submit. If not specified, you may be prompted to select a region
* python-version: Version of Python used during training. If not set, the default version is 2.7. Python 3.5 is available when runtime_version is set to 1.4 and above. Python 2.7 works with all supported runtime versions
* scale-tier: Specify the machine types, the number of replicas for workers, and parameter servers
* config_file: Specify name of the configuration file to be used by the model
```


### train_local.sh

This script train model on your local machine

#### Arguments:
```
* package-path: Specify path where package is stored
* module-name: Specify path to the module file
* config_file: Specify name of the configuration file to be used by the model
```



# testing_markdown