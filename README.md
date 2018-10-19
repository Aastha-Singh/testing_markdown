
# FCA Powertrain Calibration

* Checkpoints: contains checkpoints (.ckpt) created during the training process.
* Logs: contains the log and summary files generated during training & testing process.
* Model: contains different models used in the projects.
* Model_data: contains different configuration files (.pbtxt, cfg, json) used for training and inference which includes hyperparameters of model like  learning rate, batch size etc. Also there can be different versions of these files to try out different setting with different hardware.
* Src: contains training, inference and benchmarking scripts
* Utils: contains utility functions used for preprocessing and postprocessing of data.
* Weights: contains all the weights (.npz, .pb) used for inference

## Description for scripts

### create_package.sh

This script automatically creates package to be used to train model either on local or on cloud.

#### Example
```
python3 create_package.py --package_name multitask \
	--config_file multitask_config_cloud.py \
	--utils_file read_tfrecord.py \
	--main_file trainer_cnn.py \
	--model_file cnn_model.py \
	--cloud True
```

#### Arguments

* **package_name**: Specify name of the package
* **config_file**: Specify name of the configuration file to used to train the model
* **utils_file**: Specify name of the utils file to used to train the model
* **main_file**: Specify name of the main file to used to train the model
* **model_file**: Specify name of the model file to used to train the model
* **cloud**: This will be _True_ if package is to be used on cloud, otherwise _False_


### train_cloulml.sh


This script train model on Google Cloud ML.

#### Example
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

#### Arguments

* **job**: It is optional to give job name else it will take default name
* **stream-logs**: Block until job completion and stream the logs while the job runs
* **runtime-version**: Google Cloud ML Engine runtime version for this job
* **staging-bucket**: Bucket in which to stage training archives
* **module-name**: Name of the module to run
* **packages**: Path to Python archives used for training
* **region**: Region of the machine learning training job to submit. If not specified, you may be prompted to select a region
* **python-version**: Version of Python used during training. If not set, the default version is 2.7. Python 3.5 is available when runtime_version is set to 1.4 and above. Python 2.7 works with all supported runtime versions
* **scale-tier**: Specify the machine types, the number of replicas for workers, and parameter servers
* **config_file**: Specify name of the configuration file to be used by the model




### train_local.sh

This script train model on your local machine

#### Example
```
gcloud ml-engine local train 
	--package-path=../package/local/multitask-0.1.tar.gz \
	--module-name=multitask.src.trainer_cnn \
	--\
	--config_file=multitask.config.multitask_config_local
```

#### Arguments

* **package-path**: Specify path where package is stored
* **module-name**: Specify path to the module file
* **config_file**: Specify name of the configuration file to be used by the model
