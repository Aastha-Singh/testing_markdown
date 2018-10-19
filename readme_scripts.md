### create_package.sh

This script automatically creates package to be used to train model either on local or on cloud.

#### Example:
```
python3 create_package.py --package_name multitask \
	--config_file multitask_config_cloud.py \
	--utils_file read_tfrecord.py \
	--main_file trainer_cnn.py \
	--model_file cnn_model.py \
	--cloud True
```

#### Arguments:
```
1. package_name: Provide name of the package
2. config_file: Provide name of the configuration file to used to train the model
3. utils_file: Provide name of the configuration file to used to train the model
4. main_file: Provide name of the configuration file to used to train the model
5. model_file: Provide name of the configuration file to used to train the model
6. cloud: This will be "True" if package is to be used on cloud, otherwise "False"
```



### train_cloulml.sh


This script train model on Google Cloud ML.

#### Example:
```
gcloud ml-engine jobs submit training $JOB_NAME \
	--stream-logs \
	--runtime-version 1.9 \
	--staging-bucket gs://powertrain \
	--module-name multitask.src.trainer_cnn \
	--packages ../package/cloud/multitask-0.1.tar.gz \
	--region us-central1 \
	--python-version 3.5 \
	--scale-tier BASIC \
	--\
	--config_file multitask.config.multitask_config_cloud
```

#### Arguments:
```
1. **job**: It is optional to give job name else it will take default name
2. stream-logs: Block until job completion and stream the logs while the job runs
3. runtime-version: Google Cloud ML Engine runtime version for this job
4. staging-bucket: Bucket in which to stage training archives
5. module-name: Name of the module to run
6. packages: Path to Python archives used for training
7. region: Region of the machine learning training job to submit. If not specified, you may be prompted to select a region
8. python-version: Version of Python used during training. If not set, the default version is 2.7. Python 3.5 is available when runtime_version is set to 1.4 and above. Python 2.7 works with all supported runtime versions
9. scale-tier: Specify the machine types, the number of replicas for workers, and parameter servers
10. config_file: Specify name of the configuration file to be used by the model
```



### train_local.sh

This script train model on your local machine

#### Example:
```
gcloud ml-engine local train 
	--package-path=../package/local/multitask-0.1.tar.gz \
	--module-name=multitask.src.trainer_cnn \
	--\
	--config_file=multitask.config.multitask_config_local
```

#### Arguments:
```
1. package-path: Specify path where package is stored
2. module-name: Specify path to the module file
3. config_file: Specify name of the configuration file to be used by the model
```
