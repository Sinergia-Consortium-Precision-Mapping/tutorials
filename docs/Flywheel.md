


# FLYWHEEL


Flywheel is a commercial data imaging data plaftorm.

[CIBM](https://cibm.ch/the-center/) launched its Flywheel platform in 2023 with a one year pilot test. 

We dispose of storage space on the platform for some data.
We will use it to store the prospective data of the SINERGIA project.


## How to access Flywheel 

To access the flywheel CIBM platform, you can in your web browser use the following adress:

```py
	flywheel.cibm.ch
```

To connect, you need to us your switch edu-ID profile. 
The connexion requires a double authentication. 

Our space on Flywheel platform:

```py
	Lab: connectomics-lab
	Project: SINERGIA_dataset
```


### Flywheel - CLI 

### For MRI DICOMS

To include dicoms from CLI interface

```py
	fw ingest dicom path/to/dicom/directory connectomics-lab SINERGIA_dataset --subject 01 --session 01
```
 
 This should detect the number of sessions and images.
 You can check if the number is consistent with your data and the fw cli will propose you to upload or not the data. 










