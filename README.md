# man page for msb-make.
## NAME 
**msb-make** scaffolds a script folder, optionally populates it with a router and packages it for publication to a debian repository.
## SYNOPSIS
**msb-make** [objectPath] [ objectId1 ... objectIdN ] -action [ actionArg1 .. actionArgM]

## DESCRIPTION 
**msb-make** manages the following object paths:  

### bashrc
Programs on the paths registered in the ~/.bashrc file can be invoked directly. Use this object path to manage the programs registered to be executable from a development environment.

### folder
This is the main object to manage. The program is a folder which consists of standardized subfolders and files.

### folder.account.domain.distrib.release
Use this path to manage the publication of a program folder.

### folder.conf-field
Use this path to manage the configuration fields in the 'build.conf' file in a folder.

### folder.release
This path is used automatically by **msb-make** during the publication of a program folder.

### folder.router
The main program is located in **src/usr/bin**. It will invoke the router and according to the object path and action supplied, execute a subordinate script located in **src/usr/share/[program]-core/subcommands**. Use this path to manage which router to use for this task. The default router is **bash-default**.

### folder.version
Use this path to manage the version of the program folder.

## OPTIONS

### --help
shows the general help paragraph.

### [objectpath] --help
shows general help for the object path.

### --version
shows the program's version.

### --license
shows the program's license.

### bashrc -remove-invalid-paths
This command checks if all the existing paths registered are still valid, and removes the invalid ones. Example:  
**msb-make** bashrc -remove-invalid-paths

### bashrc -remove-path [arg]
This command removes a folder from the execution path. Example:  
{command} bashrc -remove-path myprogram  
The 'myprogram' argument should be a folder containing a script.

### bashrc -show-paths
This command shows the paths registered in the ~/.bashrc execution path. Synopsis:**
{command} bashrc -show-paths

### bashrc -add-path [arg]
This command adds a folder to the ~/.bashrc, so that you can execute the program in the folder without specifying its path. Example:  
**msb-make** bashrc -add-path gpg-man  
This example will add the gpg-man folder to your path. You will need to source .bashrc (or re-open the terminal) again, for the changes to take effect:  
source ~/.bashrc

### folder [obj] -generate-deb-control
This program generate the Debian manifest control file. It is used by the **build** command. Example  :
**msb-make** folder myprogram -generate-deb-control

### folder [obj] -deploy-local
This program bypasses the entire packaging system to install a program locally. Example:  
sudo **msb-make** folder myprogram -deploy-local  
This command must be executed as root.


### folder [obj] -show-man-page
This command shows the manpage for a program folder. Example:  
**msb-make** folder myscript -show-man-page

### folder [obj] -show-files
This command lists the files inside the program folder. Example:  
**msb-make** folder myscript -show-files

### folder [obj] -generate-man-page
This command generates the manpage for a program folder. This command is used by the **build** command. Example:  
**msb-make** folder myprogram -generate-man-page

### folder [obj] -generate-readme
This command generates the readme page in markdown (.md) format. It is called by the **build** command. Example:  
**msb-make** folder myprogram -generate-readme

### folder [obj] -show-version
This command shows the version of a program folder. Example:  
**msb-make** folder myscript -show-version

### folder [obj] -fix-exec-perms
This command fixes all the execute permissions in the subcommands folder. Example:  
**msb-make** folder myscript -fix-exec-perms

### folder [obj] -license-exists
This command checks if the folder contains a license file. Example:  
**msb-make** folder myprogram -license-exists  
This command returns 'yes' if the license file exists and 'no' if it does not.

### folder [obj] -rename [arg]
This program renames a program folder and the internal files and folders that were named accordingly. Example:  
**msb-make** folder myscript -rename mynewscript

### folder [obj] -generate-deb-dirs
This command generates the Debian 'dirs' manifest file. It is used by the **build** command. Example:  
**msb-make** folder myprogram -generate-deb-dirs

### folder [obj] -remove-license
This command removes the license file from a program folder. Example:  
**msb-make** folder myscript -remove-license

### folder [obj] -remove-router
This command removes the router from a program folder. Example:  
**msb-make** folder myprogram -remove-router

### folder [obj] -show-license
This command shows the license installed. Example:  
**msb-make** folder myscript -show-license

### folder [obj] -undeploy-local
This command removes a rapid local deployment of a folder. Example:  
sudo **msb-make** folder myscript -undeploy-local  
This command must be executed as root.

### folder [obj] -scaffold
This command scaffolds a given program folder. If the folder does not exist, the command will create it. It creates:  
sample: the main folder  
sample/build.conf: the build configuration file  
sample/man-src: the main manpage source folder  
sample/man-src/3.DESCRIPTION: manpage section  
sample/man-src/1.NAME: manpage section  
sample/man-src/7.FILES: manpage section  
sample/man-src/6.EXIT-STATUS: manpage section  
sample/man-src/5.ENVIRONMENT: manpage section  
sample/install: installer script folder  
sample/install/postinst: the script to run after installation  
sample/install/postrm: the script to run after uninstallation  
sample/src: the source folder  
sample/src/usr: folder that matches the '/usr' folder on a linux system  
sample/src/usr/bin: main program/entry point folder  
sample/src/usr/bin/sample: the main program itself  
sample/src/usr/share: folder that matches the '/share' folder on a linux system   
sample/src/usr/share/sample-core: the main scriptbox folder  
sample/src/usr/share/sample-core/help: the help files for the scriptbox commands in the program  
sample/src/etc: matches the '/etc' folder on a linux system  
sample/src/etc/sample.d: the configuration folder for the program  


### folder [obj] -touch-help
This command generates empty a help file for each script file in the subcommands folder, for which no help file is already available. Example:  
**msb-make** myscript -touch-help

### folder [obj] -delete
This command deletes a program folder. Example  :
**msb-make** folder myprogram -delete

### folder [obj] -deb-copy
This command is used by the **-build** command to generate the readme file, generate the debian manifest files, and copy the script files to the DEBIAN package folder. Example:  
**msb-make** folder myprogram -deb-copy  

### folder [obj] -set-standard-license [arg]
This command sets a standard license on the program. Example:  
**msb-make** folder myscript -set-standard-license GPL  
This command installs the GPL license file inside the program. If you need to install a custom license file, manually copy the custom license to the program's core folder. The command also inscribes the license name in the 'build.conf' file. You can verify the license inscribed in the 'build.conf' file with the command:  
**msb-make** folder.conf-field myscript license -show  

### folder [obj] -purge-help
This command removes all empty help files from the help folder. Example:  
**msb-make** folder myprogram -purge-help

### folder [obj] -show-conf-fields
This command shows the configuration fields available in the 'build.conf' file with their values. Example:  
**msb-make** folder myscript -show-conf-fields

### folder.account.domain.distrib.release.arg.arg.arg.arg [obj] -unpublish
This command unpublishes a folder from a remote server. Synopsis:  
**msb-make** folder.account.domain.distrib.release [folder] [account] [domain] [distrib] [release] -unpublish  
Example:  
**msb-make** folder.account.domain.distrib.release myprogram john@doe.com garagesoft.com ubuntu precise -unpublish

### folder.account.domain.distrib.release.arg.arg.arg.arg [obj] -publish
This command publishes a folder to a remote repository. Synopsis:  
**msb-make** folder.account.domain.distrib.release [folder] [account] [domain] [distrib] [release] -publish  
Example:  
**msb-make** folder.account.domain.distrib.release myprogram john@doe.com garagesoft.com ubuntu precise -publish  

### folder.conf-field.arg [obj] -set [arg]
This command sets the value for a configuration field in the 'build.conf' file. Example:  
**msb-make** folder.conf-field myscript author_name -set "John Doe"  
You can also just edit the 'build.conf' file and set the values of the fields directly.
To set a blank value, supply the value 'null'. Example:  
**msb-make** folder.conf-field myscript author_name -set null  
To set a 'null' value, supply the value '|null'. Example:  
**msb-make** folder.conf-field myscript author_name -set '|null'  
To set a '|null' value, supply the value '||null'. Example:  
**msb-make** folder.conf-field myscript author_name -set '||null'  
To set a value of 'null' preceded by k times '|', prefix the '|' character k+1 times.

### folder.conf-field.arg [obj] -show
This command shows the value of a configuration field in a folder. Example:  
**msb-make** folder.conf-field myscript email_signature -show

### folder.release.arg [obj] -clean
This command removes the packages built. Example:  
**msb-make** folder.release myscript precise -clean

### folder.release.arg [obj] -generate-deb-changelog
This command generates a Debian manifest changelog file. It is called automatically by the 'build' command. Example:  
**msb-make** folder.release myscript precise -generate-deb-changelog

### folder.release.arg [obj] -build
This command builds the package for a folder for a particular release. Example:  
**msb-make** folder.release myscript precise -build

### folder.router.arg [obj] -populate
This command populates a folder with a standard router. Example:  
**msb-make** folder.router myscript bash-default -populate


### folder.version.arg [obj] -set
This command sets the version for a program folder. Example:  
**msb-make** folder.version myscript 0.8.3 -set

## ENVIRONMENT 
## EXIT-STATUS 
### 0
A zero exit code means that everything went ok.
### 1
A one exit code is usually an error generated by **msb-make** itself.
### other
Another exit code is always an error generated by one of the underlying programs invoked by **msb-make**.

## FILES 
## AUTHOR
Erik Poupaert <erik@sankuru.biz>

## REPORTING-BUGS
Report bugs to: erik@sankuru.biz

# COPYRIGHT
Licensed under GPL
