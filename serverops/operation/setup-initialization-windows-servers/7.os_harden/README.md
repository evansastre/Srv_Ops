# 7.OS\_Harden

1.All server get executable files from salt master  
salt -N 'OS-Windows' cp.get\_file [salt://security\_policy\_command.bat](salt://security_policy_command.bat) 'D:\security\_policy\_command.bat'  
salt -N 'OS-Windows' cp.get\_file [salt://security\_policy\_infchange.inf](salt://security_policy_infchange.inf) 'D:\security\_policy\_infchange.inf'

  
2.Execute   
salt -N 'OS-Windows' cmd.run 'pushd D:\ && security\_policy\_command.bat'

  
3.Confirm result  
can check by check list

  
4.delete files  
salt -N 'OS-Windows' cmd.run 'del D:\security\_policy\_command.bat'  
salt -N 'OS-Windows' cmd.run 'del D:\security\_policy\_infchange.inf'  
salt -N 'OS-Windows' cmd.run 'del D:\secedit.sdb'

