# PatchDetection Pipeline
This readme describes the deployment and execution of a Docker image, which contains the software that was used to generate the data published in the manuscript *Structures and functions linked to genome-wide adaptation of human influenza A viruses*. The image is available for Linux, Windows and Mac systems. Follow the steps below according to your operating system to use the pipeline yourself.

**Contents of this Readme:**
+ PatchDetection on Linux
	+ Requirements
	+ Input Data
	+ Running the Pipeline 
+ PatchDetection on Windows
	+ Requirements
	+ Input Data
	+ Running the Pipeline 
+ PatchDetection on MAC
	+ Requirements
	+ Input Data
	+ Running the Pipeline 
+ Output Files
+ Docker Advanced
+ Questions and Bug Reports

- - -
## PatchDetection on Linux
### 1) Requirements

The software runs on Docker. Docker is an open platform for developers and sysadmins to build, ship, and run distributed applications. It is available for a number of Linux distributions like Ubuntu, Debian or Fedora.

1. **Install Docker**, if it is not already installed on your machine. Docker is available under [DockerStore (Community Edition)](https://store.docker.com/search?type=edition&offering=community "Docker Store") (the free community edition is sufficient). Please follow the instructions on the respective download page.

### 2) Input Data
1. **Create a folder called *patchdetection*,** or, if you've run the pipeline before, you can re-use the old *patchdetection*-folder. It does not matter where this folder is located on your machine, but it must be named *patchdetection*. The docker container will mount this folder to access the data that is located in there. 
2. **Copy a folder named *[PREFIX]* that contains the files to be analyzed into the *patchdetection* folder.** The files in the *[PREFIX]*-folder must be named *[PREFIX]_cds.fa* and *[PREFIX]_aa.fa, where *[PREFIX]* can be any character sequence. The prefix must be the same!
> Please note that sequences without a full date (formatted as either yyyy-mm-dd or yyyy/mm/dd) will be ignored by the pipeline.
> Identifiers in the cds-file must match the identifiers for the respective aa-sequence in the aa-file.
> For a reference file of how *[PREFIX]_cds.fa* should look like, please refer to [this folder](https://github.com/hzi-bifo/SDplots/blob/master/Software/Testdata/HA_cds.fa "HA_cds.fa").

### 3) Running the Pipeline
1. To run the PatchDetection pipeline, **open a command-line terminal and insert**:
		
		$sudo docker run -v [Complete/path/to/your/local/folder/]patchdetection:/app/patchdetection tklingenbifolab/pdpipeline:beta -i [PREFIX] -d [DELTA] -p [PDB FILE] [OTHER OPTIONS (see CMD Config below)]
		
2. To **customize your pipeline-deployment**, you can append the following to the run-command:
> 

	-d, --d   : delta radius, mendatory
	-c, --c   : name of the chain, default is chain A
	-p, --p   : name of the pdb file, mandatory
	-i, --i   : name of the input folder, mandatory
	-s, --s   : start Subsampling, default is false
	-h, --h   : show help (shows this list)

3. **Example**

Say the input folder [(example can be downloaded here)](https://github.com/hzi-bifo/SDplots/blob/master/Software/Testdata/HA_cds.fa "HA_cds.fa") is located in */home/johndoe/patchdetection/HA_test*, the radius is 7 angstrom and the pdb file is named 3hmg.pdb. You would then run

 	$sudo docker run -v /home/johndoe/patchdetection:/app/patchdetection tklingenbifolab/pdpipeline:beta -i HA_test -d 7 -p 3hmg.pdb

4. **Stopping the Pipeline**

If you want to terminate the pipeline, you have two options:
1. Close the terminal in which the pipeline is running (ignore the warning that might pop up).
2. More elegant: Open a second terminal, run `$sudo docker ps` and copy the container ID of the execution that you want to stop. Then run `$sudo docker stop [CONTAINER ID]`. It may take a few seconds befor the container terminates.

- - -
## PatchDetection for Windows
### 1) Requirements

The software image runs on Docker. Docker is an open platform for developers and sysadmins to build, ship, and run distributed applications. It's available for Windows 10 Professional and Enterprise.

1. **Install Docker**, if it is not already installed on your machine. Docker is available under [DockerStore (Community Edition)](https://store.docker.com/search?type=edition&offering=community "Docker Store") (the free community edition is sufficient). Please follow the instructions on the respective download page.
 
### 2) Input Data
1. **Create a folder called *patchdetection*,** or, if you've run the pipeline before, you can re-use the old *patchdetection*-folder. It does not matter where this folder is located on your machine, but it must be named *patchdetection*. The docker container will mount this folder to access the data that is located in there. 
2. **Copy a folder named *[PREFIX]* that contains the files to be analyzed into the *patchdetection* folder.** The files in the *[PREFIX]*-folder must be named *[PREFIX]_cds.fa* and *[PREFIX]_aa.fa, where *[PREFIX]* can be any character sequence. The prefix must be the same!
> Please note that sequences without a full date (formatted as either yyyy-mm-dd or yyyy/mm/dd) will be ignored by the pipeline.
> Identifiers in the cds-file must match the identifiers for the respective aa-sequence in the aa-file.
> For a reference file of how *[PREFIX]_cds.fa* should look like, please refer to [this folder](https://github.com/hzi-bifo/SDplots/blob/master/Software/Testdata/HA_cds.fa "HA_cds.fa").

### 3) Running the Pipeline
1. You need to **share the drive** that contains the *patchdetection*-folder in the Docker Settings (see [Shared Drives](https://docs.docker.com/docker-for-windows/#docker-settings "Docker Settings")). It's sufficient if you do this once the first time you use the pipeline.
2. To run the PatchDetection pipeline, **open your PowerShell as admin and insert**:
		
		$docker run -v [Complete/path/to/your/local/folder/]patchdetection:/app/patchdetection tklingenbifolab/pdpipeline:beta -i [PREFIX] -d [DELTA] -p [PDB FILE] [OTHER OPTIONS (see CMD Config below)]
		
3. To **customize your pipeline-deployment**, you can append the following to the run-command:
> 

	-d, --d   : delta radius, mendatory
	-c, --c   : name of the chain, default is chain A
	-p, --p   : name of the pdb file, mandatory
	-i, --i   : name of the input folder, mandatory
	-s, --s   : start Subsampling, default is false
	-h, --h   : show help (shows this list)

4. **Example**

Say the input folder [(example can be downloaded here)](https://github.com/hzi-bifo/SDplots/blob/master/Software/Testdata/HA_cds.fa "HA_cds.fa") is located in */home/johndoe/patchdetection/HA_test*, the radius is 7 angstrom and the pdb file is named 3hmg.pdb. You would then run

	$docker run -v C:\users\johndoe\Documents\patchdetection:\app\patchdetection tklingenbifolab/pdpipeline:beta -i HA_test -d 7 -p 3hmg.pdb

5. **Stopping the Pipeline**

If you want to terminate the pipeline, you have two options:
1. Close the terminal in which the pipeline is running (and ignore warnings that might pop up).
2. More elegant: Open a second terminal as admin, run `$docker ps` and copy the container ID of the execution that you want to stop. Then run `$docker stop [CONTAINER ID]`. It may take a few seconds befor the container terminates.
---
## PatchDetection on Mac
### 1) Requirements

The software image runs on Docker. Docker is an open platform for developers and sysadmins to build, ship, and run distributed applications. It's available for OS X El Capitan 10.11 and newer macOS releases.

1. **Install Docker**, if it is not already installed on your machine. Docker is available under [DockerStore (Community Edition)](https://store.docker.com/search?type=edition&offering=community "Docker Store") (the free community edition is sufficient). Please follow the instructions on the respective download page.
 
### 2) Input Data
1. **Create a folder called *patchdetection*,** or, if you've run the pipeline before, you can re-use the old *patchdetection*-folder. It does not matter where this folder is located on your machine, but it must be named *patchdetection*. The docker container will mount this folder to access the data that is located in there. 
2. **Copy a folder named *[PREFIX]* that contains the files to be analyzed into the *patchdetection* folder.** The files in the *[PREFIX]*-folder must be named *[PREFIX]_cds.fa* and *[PREFIX]_aa.fa, where *[PREFIX]* can be any character sequence. The prefix must be the same!
> Please note that sequences without a full date (formatted as either yyyy-mm-dd or yyyy/mm/dd) will be ignored by the pipeline.
> Identifiers in the cds-file must match the identifiers for the respective aa-sequence in the aa-file.
> For a reference file of how *[PREFIX]_cds.fa* should look like, please refer to [this folder](https://github.com/hzi-bifo/SDplots/blob/master/Software/Testdata/HA_cds.fa "HA_cds.fa").

### 3) Running the Pipeline
1. You need to **share the folder** that contains the *patchdetection*-folder in the Docker Settings (see [File Sharing](https://docs.docker.com/docker-for-mac/#file-sharing "Docker for Mac")). It's sufficient if you do this once the first time you use the pipeline.
2. To run the PatchDetection pipeline, **open a command-line terminal and insert**:
		
		$sudo docker run -v [Complete/path/to/your/local/folder/]patchdetection:/app/patchdetection tklingenbifolab/patchdetection:beta -i [PREFIX] -d [DELTA] -p [PDB FILE] [OTHER OPTIONS (see CMD Config below)]
		
3. To **customize your pipeline-deployment**, you can append the following to the run-command:
> 

	-d, --d   : delta radius, mendatory
	-c, --c   : name of the chain, default is chain A
	-p, --p   : name of the pdb file, mandatory
	-i, --i   : name of the input folder, mandatory
	-s, --s   : start Subsampling, default is false
	-h, --h   : show help (shows this list)

4. **Example**

Say the input folder [(example can be downloaded here)](https://github.com/hzi-bifo/SDplots/blob/master/Software/Testdata/HA_cds.fa "HA_cds.fa") is located in */home/johndoe/patchdetection/HA_test*, the radius is 7 angstrom and the pdb file is named 3hmg.pdb. You would then run

 	$docker run -v /Users/johndoe/Documents/patchdetection:/app/patchdetection tklingenbifolab/pdpipeline:beta -i HA_test -d 7 -p 3hmg.pdb

5. **Stopping the Pipeline**

If you want to terminate the pipeline, you have two options:
1. Close the terminal in which the pipeline is running (and ignore warnings that might pop up).
2. More elegant: Open a second terminal as admin, run `$docker ps` and copy the container ID of the execution that you want to stop. Then run `$docker stop [CONTAINER ID]`. It may take a few seconds befor the container terminates.
---
## Output Files

The output is written into a new folder named by the `-o`-parameter, for example *test_run*. If there is already a folder named this way, the pipeline will tell you to pick a different name and terminate. This allows you to run multiple executions parallel on your machine if you need to. The folder is located in the *patchdetection*-folder you created earlier. The original input-file remains in the *patchdetection*-folder but is also copied into your output folder.

The output consists of the following files:
	
* **data.significant_positions.pdf**  SD plots of the significant positions
* **data** This folder contains the input data as well as intermediate data generated during the calculation.
* **output**  This folder contains further output and provides statistics about the frequencies of sweep-related changes.
    * **data.all_positions.pdf** SD plots of all positions
* **positionplots** This folder contains SD plots for every single position. If no amino acid change is detected at a position, the respective position plot will be empty.

---
## Docker Advanced
If you want to control the usage of resources of the running software, please refer to [Docker Runtime Constraints on Resources](https://docs.docker.com/engine/reference/run/#runtime-constraints-on-resources "docs.docker.com").

---
## Questions and Bug Reports
If you have questions about the PatchDetection pipeline or bugs to report, please contact Thorsten Klingen at thorsten.klingen@helmholtz-hzi.de.

