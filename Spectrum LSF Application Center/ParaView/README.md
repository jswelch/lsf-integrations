# ParaView Template
ParaView directory include all files required for integrating openfoam 6 Paraview with IBM Spectrum LSF and IBM Spectrum LSF Application Center.
This integration is based on public docker image: openfoam/openfoam6-paraview54, there is no need to install openfoam application.

## Prerequisites
1). IBM Spectrum LSF 10.1 or above version is installed.

2). IBM Spectrum Application Center 10.2 or above version is installed.

3). LSF Compute Server support docker engine 1.12 or above version.

4). OpenFOAM template is installed into Application Center

## Deployment Steps
Step 1: download all the files under this directory ParaView/,   and copy over to IBM Spectrum LSF Application Center configuration 
        directory, for example:  /opt/ibm/lsfsuite/ext/gui/conf/application/draft/ParaView, make sure files owner are administrator, 
        all files have excutable permission.
        
Step 2: copy ParaView/startParaView  to  JOB_REPOSITORY_TOP/startParaView, make sure it is executable.  JOB_REPOSITORY_TOP is the same
        directory with template OpenFOAM,  it must be shared by all LSF servers.
	
Step 3: Configure LSF to define LSF Resource "ParaView" and assign the available Hosts to this resource
        
Step 4: restart LSF:   
        #lsfrestart
        
Step 5: logon LSF Application Center as administrator,  find and edit the template "ParaView", replace JOB_REPOSITORY_TOP with the real 
        directory introduced in Step 2 for input: "Application Command" and "Application Command to open an input file",  save and 
        publish the template.  Go to "System&Setting"-> User Role& Permission -> assign view permission of ParaView to "Normal User"

Step 6: Test case 1:  logon Application Center as a normal user, go to "+ New Workload", click on "Paraview",  a new browser window
        should show up with Paraview console running inside.
        Test case 2: logon Application Center as a normal user, submit a OpenFOAM job,  in the workload list, click on the job ID to open
        this job's details, click on "Data" tab, search and select  XXX.foam file, then click on the menu: Open with application, select
        ParaView.   an new browser window should be opened, and Paraview console is running with the current job's data opened.