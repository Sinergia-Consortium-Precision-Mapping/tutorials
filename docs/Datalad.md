



# Datalad Workflow


[Datalad](https://www.datalad.org/) is an open-source data management solution based on Git and Git-Annex.

Particularly, it can:  

- Keep track of your data  
- Create structure  
- Ensure reproducibility  
- Supports collaboration  


## Install DataLad



## Basic commands with DataLad

All the possible commands and possibilities with DataLad are exhaustively explained in the [DataLad Handbook](https://handbook.datalad.org/en/latest/)


### Create a datalad dataset from your local dataset

1. Download  locally a small dataset from OpenNeuro

``` py
    # Create the directory
    mkdir neuro-data-s3

    # Download the data
    wget https://www.fil.ion.ucl.ac.uk/spm/download/data/MoAEpilot/MoAEpilot.bids.zip -O neuro-data-s3.zip

    # Unzip the data
    unzip neuro-data-s3.zip -d neuro-data-s3

    # Move the data
    rm neuro-data-s3.zip && cd neuro-data-s3 
    mv MoAEpilot/* . && rm -R MoAEpilot
```


2. Turn local dataset into a DataLad Dataset

In your local directory with your data:

``` py
    # Start datalad tracking on the dataset
    datalad create --force --description "Neurodata to host on Github and Curnagl"

    # Check the status of datalad
    datalad status

    # Save your first change, adding the data
    datalad save -m "Add public data"

    datalad status
```



## Make the full dataset available to the SINERGIA consortium


### Note on the infrastructure 

Because of the restricitions related to the storage of sensitive data imposed by UNIL, it is unfortunately no possible yet to implement DataLad on Urblauna.
However, DataLad should be used for data provenance and tracking of all the data stored on Curnagl. 

![unildat](img/UNILstorageSpecs.png){width=45%}

### Create a sibling dataset on Curnagl and Github

#### Create the RIA store on Curnagl

In your local directory (for example, in the neuro-s3-data directory from the previous section)

``` py
        # Show all the existing siblings
        datalad siblings

        # Create a RIA store to store all the annex from Git-Annex on Curnagl
        datalad create-sibling-ria -s ANNEX_DIR ria+ssh://emullier@curnagl.dcsr.unil.ch:/work/PRTNR/CHUV/RADMED/phagmann/sinergia2norm/datalad_test --storage-sibling only
```

You can check on Curnagl, the directory 'datalad_test' should have been created. 


#### Create a sibling (without annex) on Github

In your local directory again:

``` py
    # Show all the existing siblings
    datalad siblings

    # Create the datalad sibling linked to the RIA store on Curnagl
    datalad create-sibling-github -d . TEST_DATALAD --publish-depends ANNEX_DIR -s github_sibling --credential your_github_token --github-organization sinergia-consortium-precision-mapping

    # Check if the datalad github sibling has been created
    datalad siblings

    # Push the data
    datalad push --to github_sibling
```


### Create a sibling dataset on Curnagl only


Create only one sibling on Curnagl

``` py
        # Show all the existing siblings
        datalad siblings

        # Create a RIA store to store all the annex from Git-Annex on Curnagl
        datalad create-sibling-ria -s ANNEX_DIR ria+ssh://emullier@curnagl.dcsr.unil.ch:/work/PRTNR/CHUV/RADMED/phagmann/sinergia2norm/datalad_test --new-store-ok --alias TEST_DATALAD
```

Clone the sibling

Clone the dataset from the ria stora of curnagl using the alias name  
(Without alias name, the dataset can be clone from the dataset ID).  

``` py
        datalad clone ria+ssh://emullier@curnagl.dcsr.unil.ch:/work/PRTNR/CHUV/RADMED/phagmann/sinergia2norm/datalad_test#~TEST_DATALAD
```


### Create a DataLad environment on Curnagl

Git-Annex and DataLad are not installed on Curnagl.  
However, python and miniconda are, it is then possible to create an environement in which we can install DataLad and its requirements.

#### With Python

To create the python environment
``` py
    # Load the necessary packages on Curnagl
    module load gcc python
    # Install Datalad via Pip
    python -m pip install datalad
    # Create the environment datalad
    python3 -m env /users/emullier/ENVS/datalad
```


To activate/deactive the environment
``` py
    # Activate the environment
    source /users/emullier/ENVS/datalad/bin activate
    # Deactivate the enviromment
    deactivate
```

#### With Miniconda3

Create an environment accesible from Urblauna.  
On Urblauna, the partition /work from Curnagl is mounted in read-only.  
If you want to conda environment you are creating to be useable on Urblauna, the environment needs to be created on Curnagl in the /work partition.  

``` py
    ### Creation on Curnagl only
    # Load the necessary packages on Curnagl
    module load gcc miniconda3
    # Create the conda enviromnent in the /work directory
    conda create --prefix /work/PRTNR/CHUV/RADMED/phagmann/soft/conda_envs_2/datalad_env
    ### Activation on Curnagl and/or Urblauna
    # Activate the environment
    source activate  /work/PRTNR/CHUV/RADMED/phagmann/soft/conda_envs_2/datalad_env
    # Deactivate 
    conda deactivate 
```


To activate/deactive the environment conda datalad_env
``` py
    # Load the necessary packages on Curnagl
    module load gcc miniconda3
    # Initialize conda
    conda init bash
    # Reinitialize bash
    exec bash
    # Display the list of existing environments
    conda env list
    # Activate the environment
    conda activate datalad_env
    # Deactivate the enviromment
    deactivate
```

### A glance on the final configuration

You can check if all your siblings are correctly set and if the data are stored correctly on Github and Curnagl.

![dataladfinal](img/FinalViewDataladCurnagl.png){width=70%}



### Step-by-Step in video

![type:video](./tutos_videos/Tuto_Datalad_AnnexCurnagl.mp4)

