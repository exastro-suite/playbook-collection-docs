# Cautionary Notes

* If you want to use the following roles with Exastro IT Automation, you need to directly enter the values of multiple variables in json format for some parameter items.  
  * Role: RH_grub2/OS_build  
    * ITA readme : ita_readme_OS-RHEL8%RH_grub2%OS_build.yml  
    * Parameter : VAR_RH_grub2.properties  
    * the sample of json content :   {'GRUB_DISABLE_RECOVERY': '"true"','GRUB_DISABLE_SUBMENU': 'true'}
  * Role: RH_selinux/OS_build  
    * ITA readme : ita_readme_OS-RHEL8%RH_selinux%OS_build.yml  
    * Parameter : VAR_RH_selinux.properties  
    * the sample of json content :   {'SELINUX': enforcing,'SELINUXTYPE': targeted}
  * Role: RH_sysctl/OS_build  
    * ITA readme : ita_readme_OS-RHEL8%RH_sysctl%OS_build.yml  
    * Parameter : VAR_RH_sysctl.properties  
    * the sample of json content :   {'kernel.panic': '10','kernel.unknown_nmi_panic': '0'}
  * Role: RH_systemd/OS_build  
    * ITA readme : ita_readme_OS-RHEL8%RH_systemd%OS_build.yml  
    * Parameter : VAR_RH_systemd.value.properties  
    * the sample of json content :   {'JoinControllers': 'cpu,cpuacct net_cls,net_prio','LogColor': 'yes','LogLevel': info,'LogLocation': 'no','LogTarget': journal-or-kmsg}
  * Role: RH_vsftpd/OS_build  
    * ITA readme : ita_readme_OS-RHEL8%RH_vsftpd%OS_build.yml  
    * Parameter : VAR_RH_vsftpd.properties  
    * the sample of json content :   {'listen': 'NO','listen_ipv6': 'YES'}
