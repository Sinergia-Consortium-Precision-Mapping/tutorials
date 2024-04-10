




# BIDS Organization


## What is BIDS?

Brain Imaging Data Structure

Full BIDS specification: [https://bids-specification.readthedocs.io/](https://bids-specification.readthedocs.io/en/stable/)

- By modalities used in the consortiun:
    - for [MRI data](https://bids-specification.readthedocs.io/en/stable/04-modality-specific-files/01-magnetic-resonance-imaging-data.html)
    - for [EEG data](https://bids-specification.readthedocs.io/en/stable/04-modality-specific-files/03-electroencephalography.html) 


### Tools for Data Conversion

- For MRI data:  
    - Heudiconv  
        - [GitHub](https://github.com/nipy/heudiconv)  
        - [Documentation](https://heudiconv.readthedocs.io/en/latest/)
    - Dicom2niix
        - [GitHub](https://github.com/rordenlab/dcm2niix)
    - Dicom2bids    
        - [GitHub](https://github.com/UNFmontreal/Dcm2Bids)
    - Bidskit
        - [GitHub](https://github.com/jmtyszka/bidskit)

    
- For EEG  



## An Example: Convert MRI data to BIDS with heudiconv 

Full heudiconv documentation: https://heudiconv.readthedocs.io/en/latest/ 


### Setting up your heudiconv pipeline

Put your DICOMS directory in a sub-XXX/ses-XXX directory such as:

```py
	/home/localadmin/Documents/BIDS/sub-01/ses-001/DICOMS
```

Use heudiconv to extract the information about the sequences from a DICOMs directory
```py
	docker run --rm -it -v /home/localadmin/Documents:/base nipy/heudiconv:latest -d /base/BIDS/sub-{subject}/ses-{session}/DICOMS/*.dcm -o /base/Nifti -f convertall -s 01 -ss 001 -c none -–overwrite 
```

If the data are in the old biotech format such as for example:
```py
    /home/localadmin/DATA/RAW_DATA/RAW_7T_Acquisitions/sub-FCBT001724/ses-20240122140245/
```

then the command can be adapted as:

```py
    docker run --rm -it -v /home/localadmin/DATA/RAW_DATA/RAW_7T_Acquisitions/:/base nipy/heudiconv:latest -d /base/sub-{subject}/ses-{session}/*/*/*/*  -o /base/Nifti -f convertall -s 01 -ss 1 -c none --overwrite
```


It generates a hidden folder .heudiconv in which you will be able to find a dicominfo.tsv file that you can open with a spreadsheet software such as Excel. 


Image of excel file (?)


Create your heuristic.py file from the information extracted and BIDS specification

1. Using this and the BIDS specification (https://bids-specification.readthedocs.io/en/stable/ ) you can automatize the conversion and name specification to automatically create your BIDS dataset. 

2. Start from a template heuristic.py (for templates: https://github.com/nipy/heudiconv/tree/master/heudiconv/heuristics ) and adapt it for your sequence names and your BIDS directory. 

image of the heuristic file (?)


add video (?)

### Conversion with heudiconv

Then when you are ready you can proceed to the actual conversion using your own heuristic.py file using this docker command line:

Use heudiconv to extract the information about the sequences from a DICOMs directory
```py
    docker run --rm -it -v /home/localadmin/Documents:/base nipy/heudiconv:latest -d /base/BIDS/sub-{subject}/ses-{session}/DICOMS/*.dcm -o /base/Nifti -f /base/Nifti/code/heuristic.py -s 01 -ss 001 -c dcm2niix -b –overwrite 
```

Finally you get, with this command,  your BIDS directory in the Nifti directory. 


add video (?)


### BIDS validator

To check the validity and integrity you can take your dataset to the BIDS validator. There exists an online version ‘online BIDS validator’ (https://bids-standard.github.io/bids-validator/ ) or via the Docker App BIDS/validator. 


```py
    docker run -ti --rm -v /path/to/data:/data:ro bids/validator /data
```

It will indicate to you the warnings and fatal errors to fix in order to be able to pass your dataset through the BIDS-app of your choice. 

add video (?)



