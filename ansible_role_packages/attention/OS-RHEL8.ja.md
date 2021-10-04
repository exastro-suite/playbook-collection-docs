# 注意事項

* Exastro IT Automation（以降、ITAと表記）で以下のロールを利用する場合、一部のパラメータ項目については[代入値管理]画面から複数の変数の値を直接json形式で入力する必要があります。 
  * ロール ： RH_grub2/OS_build  
    * ITA readmeファイル名 ： ita_readme_OS-RHEL8%RH_grub2%OS_build.yml  
    * パラメータ項目名 ： VAR_RH_grub2.properties  
    * json形式の具体値の例 ：  {'GRUB_DISABLE_RECOVERY': '"true"','GRUB_DISABLE_SUBMENU': 'true'}
  * ロール ： RH_selinux/OS_build  
    * ITA readmeファイル名 ： ita_readme_OS-RHEL8%RH_selinux%OS_build.yml  
    * パラメータ項目名 ： VAR_RH_selinux.properties  
    * json形式の具体値の例 ：  {'SELINUX': enforcing,'SELINUXTYPE': targeted}
  * ロール ： RH_sysctl/OS_build  
    * ITA readmeファイル名 ： ita_readme_OS-RHEL8%RH_sysctl%OS_build.yml  
    * パラメータ項目名 ： VAR_RH_sysctl.properties  
    * json形式の具体値の例 ：  {'kernel.panic': '10','kernel.unknown_nmi_panic': '0'}
  * ロール ： RH_systemd/OS_build  
    * ITA readmeファイル名 ： ita_readme_OS-RHEL8%RH_systemd%OS_build.yml  
    * パラメータ項目名 ： VAR_RH_systemd.value.properties  
    * json形式の具体値の例 ：  {'JoinControllers': 'cpu,cpuacct net_cls,net_prio','LogColor': 'yes','LogLevel': info,'LogLocation': 'no','LogTarget': journal-or-kmsg}
  * ロール ： RH_vsftpd/OS_build  
    * ITA readmeファイル名 ： ita_readme_OS-RHEL8%RH_vsftpd%OS_build.yml  
    * パラメータ項目名 ： VAR_RH_vsftpd.properties  
    * json形式の具体値の例 ：  {'listen': 'NO','listen_ipv6': 'YES'}
