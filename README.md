Setting Up For Automation:

Directory to place the python script
------------------------------------
All the scripts should be placed at below location along with .p4config 

/dbc/blr-dbc<dbc_num>/<user>/workspace_<user>/vsphere65p02_<user>
e.g. /dbc/blr-dbc502/kshrimal/workspace_kshrimal/vsphere65p02_kshrimal


User password for perforce:
---------------------------
For encryption of the password
md5_digest=`perl -MDigest::MD5=md5_hex -e"print uc(md5_hex(@ARGV[0]))" <password>`
Run the above command in bash

Copy the encrypted password from md5_digest into 'key.txt' file and keep the file in the same location as the other scripts.


Config file and Encryption of password for mail and dbc 
-----------------------------------------------------------
Edit the username, encrypted passwords and mailing list in config.json file.

For mail password encryption,

1>echo <password of the mail> | openssl enc -aes-128-cbc -a -salt -pass pass:121
Copy the hashkey under ['pass']['mail'] in config file.
e.g.-U2FsdGVkX1/lXSnI4Uplc6DwDPPUQ/WjHULJoKypTO8=

For dbc password encryption

2>echo <password of the dbc> | openssl enc -aes-128-cbc -a -salt -pass pass:121
Copy the hashkey under ['pass']['dbc'] in config file.
e.g.-U2FsdGVkX1/lXSnI4Uplc6DwDPPUQ/WjHULJoKypTO8=


Package installation
--------------------
1>httplib2
/mts-blr/home/<user>/.local/bin/pip install requests --user

2>requests
/mts-blr/home/<user>/.local/bin/pip install httplib2 --user

e.g.- /mts-blr/home/kshrimal/.local/bin/pip install requests --user


For passing the Arguments in the Script if the scripts are executed Seperately
-----------------------------------------------------------------------------
1>shell.sh <oldCln> <newCln> <library> <latestVersion> <specPath> 

2>deployment.py <sbBuildNumber>
e.g. python deployment.py sb-12345 

3>verification.py <logsPath> <sbBuildNumber> <libraryName> <expectedVersion>
e.g python vaerification.py /tmp/logfiles_CloudVm 12345 vpostgres 9.4.15

4>appcheck.py <no arguments>

5>appcheck.sh <link of VIM iso file> <link of VCSA iso file>


Log Files
---------
1. output.log - Complete log

2. outputfile_<machine>.out - Based on the deployment machine selected.

3. Reports
	i>summary.txt 					- Overall report
	ii>dep_report.txt 				- Deployment report
	iii>verification_summary.txt 	- verification report
