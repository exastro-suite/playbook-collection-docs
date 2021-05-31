# Cautionary Notes

* If you want to use the following roles with Exastro IT Automation, you need to customize the ITA readme file for your environment before importing with ITA.  
  In that case, decompress the Zip file, modify the target ITA readme file, and compress it again in Zip format to make it a Roll Package.  
  * Role: WIN_NetAdapterAdvancedProperty/OS_build  
    * ITA readme : ita_readme_OS-Windows2019%WIN_NetAdapterAdvancedProperty%OS_build.yml  
    * Parameter : VAR_WIN_NetAdapterAdvancedProperty  
    * How to customize : Customize the ITA readme for your environment by referring to the examples in the role's README.md file.  
