**Repository Moved**

This repository has moved to [tseward/AWACPM](https://github.com/tseward/AWACPM).

# AWACPM
Automated Web Application Companion Patch Management (Office Web Apps 2013/Office Online Server)

A PowerShell module designed to  patch an Office Web Apps 2013 or Office Online Server 2016 farm. The process is automated on a per-machine basis, creating a new WAC farm with the previous settings applied, or joining an existing WAC farm. Note that if Editing is enabled, you will be prompted to confirm enabling it due to licensing.

Example usage:

To patch a WAC server in a farm where it will become the lead host:

    Import-Module .\AWACPM.psm1
    $patch = "\\fileserver\patches\wacserver2013-kb3115022-fullfile-x64-glb.exe"
    Start-OfficeWebAppsPatch -ConfigurationFile C:\WACConfiguration -PatchFile $patch -SetAsLeadHost $true

For all other servers, including the original lead host, run with the -MachineToJoin parameter, specifying the lead host FQDN.

    Import-Module .\AWACPM.psm1
    $patch = "\\fileserver\patches\wacserver2013-kb3115022-fullfile-x64-glb.exe"
    Start-OfficeWebAppsPatch -ConfigurationFile C:\WACConfiguration -PatchFile $patch `
        -SetAsLeadHost $false -MachineToJoin wac02.example.com

A process flow diagram is available from the [Wiki](https://github.com/Nauplius/AWACPM/wiki/Process-Diagram).

Parameters:

    -SetAsLeadHost $true 
Indicates this is the first server of the new farm.
    
    -ConfigurationFile
Indicates the location of the configuration file to export/import. Must be a valid path to a folder.
    
    -MachineToJoin
The fully qualified domain name of an existing WAC/OOS machine to join.
