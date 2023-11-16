



# DATALAD 


[Datalad](https://www.datalad.org/) is an open-source data management solution based on Git and Git-Annex.

Particularly, it can:
- Keep track of your data
- Create structure
- Ensure reproducibility
- Supports collaboration



## Basic commands with DataLad

All the possible commands and possibilities with DataLad are exhaustively explained in the [DataLad Handbook](https://handbook.datalad.org/en/latest/)


### Create a datalad dataset from your local dataset

1. Download  locally a small dataset from OpenNeuro

    mkdir neuro-data-s3

    wget https://www.fil.ion.ucl.ac.uk/spm/download/data/MoAEpilot/MoAEpilot.bids.zip -O neuro-data-s3.zip

    unzip neuro-data-s3.zip -d neuro-data-s3

    rm neuro-data-s3.zip && cd neuro-data-s3 

    mv MoAEpilot/* . && rm -R MoAEpilot




## DataLad on Curnagl

Because of the restricitions related to the storage of sensitive data imposed by UNIL, it is unfortunately no possible yet to implement DataLad on Urblauna.
However, DataLad should be used for data provenance and tracking of all the data stored on Curnagl. 

![unildat](img/UNILstorageSpecs.png){width=30%}



