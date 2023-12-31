﻿


# Connexion to UNIL storage

## UNIL Storage Spaces

Two storage spaces are available on UNIL servers to store the project's data.


### **CURNAGL**: Regular Data

UNIL HPC Cluster    
For all the detailed information: [CURNAGL WIKI UNIL](https://wiki.unil.ch/ci/books/high-performance-computing-hpc/page/curnagl)  

Sinergia Directory Path
```py
	/work/PRTNR/CHUV/RADMED/phagmann/sinergia2norm
```


### **URBLAUNA**:  Sensitive Data   

UNIL Sensitive data compute cluster  
For all the detailed information: [URBLAUNA WIKI UNIL](https://wiki.unil.ch/ci/books/high-performance-computing-hpc/page/urblauna)  

Sinergia Directory Path 
```py
	# For sensitive data
	/data/PRNTR/CHUV/RADMED/phagmann/sinergia2sens
	# For archiving [Not frequent access]
	/archive/PRTNR/CHUV/RADMED/phagmann/sinergia2sens
```


## Getting the access

Getting access to UNIL servers: [UNIL Wiki Page](https://wiki.unil.ch/ci/books/high-performance-computing-hpc/page/how-to-access-the-clusters) 

Getting UNIL access following this [procedure](https://wiki.unil.ch/ci/books/high-performance-computing-hpc/page/providing-access-to-external-collaborators)  
1. If you don’t have one, create a [EduID profile](https://login.eduid.ch/idp/profile/SAML2/Redirect/SSO?execution=e1s2)  
2. Fill the form for creation of UNIL account with Patric as a sponsor  
3. Link your UNIL account and EduID profiles on [id.unil.ch](https://id.unil.ch/)  
4. Send your UNIL username to Patric  
5. Activate UNIL VPN  
6. Connect to the server  


## Connexion to UNIL VPN

- Download [Ivanti Secure Access Client](https://www.ivanti.com/products/secure-unified-client)  
- Connect using your switch edu-ID account  
- Confirm the identification on your phone using authenticator app.

## Connexion to Storage Spaces

### Curnagl  

1. Open a terminal
2. Command Line:

```py
	ssh username@curnagl.dcsr.unil.ch
```

3. Enter your UNIL password


##### Step-by-step in video 

How to connect to Curnagl:

![type:video](./tutos_videos/Tuto_Connexion_Curnagl_UNIL.mp4)


### Urblauna 

#### via Command Line
1. Open a terminal
2. Command Line:

```py
	ssh username@u-ssh.dcsr.unil.ch
```

3. Enter your UNIL password
4. Enter the verification code from your authenticator phone app

##### Step-by-step in video 

How to connect to Urblauna via Command Line:


#### via Web Interface

1. Open a web browser
2. Command Line:
	u-web.dcsr.unil.ch
3. Use your UNIL username and password
4. Enter the verification code from your authenticator phone app



## Exchange Data

### Curnagl

Copy of the data can be done via **scp** command

```py
	# For a directory
	scp -R /path/to/rep/to/copy path/to/destination
	# For a file 
	scp /path/to/rep/to/file.extension path/to/destination
```

### Urblauna

Copy of the data can be done via **sftp in the /scratch/username** directory only (scp command blocked)

```py
	# In a terminal
	sftp username@u-sftp.dcsr.unil.ch
	# Then enter your UNIL password and your verification code on the authenticator app
	## To get a directory from Urblauna to your local directory on your computer
	get -R path/to/directory
	## To get a push from your local directory on your computer to Urblauna
	put -R path/ti/directory
	# Data are pushed in /scratch/username in Urblauna

```