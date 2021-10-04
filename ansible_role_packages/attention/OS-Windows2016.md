# Cautionary Notes

* If you want to use the following roles with Exastro IT Automation, you need to directly enter the values of multiple variables in json format for some parameter items.  
  * Role: WIN_NetAdapterAdvancedProperty/OS_build  
    * ITA readme : ita_readme_OS-Windows2016%WIN_NetAdapterAdvancedProperty%OS_build.yml  
    * Parameter : VAR_WIN_NetAdapterAdvancedProperty  
    * the sample of json content :   {'vmxnet3 Ethernet Adapter':{'Enable adaptive rx ring sizing': Enabled,'IPv4 TSO Offload': Enabled}}  
