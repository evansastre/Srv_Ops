# Apply Server Patch For QA

```bash
#Server_Patch_Dev.sh
#!/bin/bash
 
/srv/salt/QA_script/GameServiceVersion/GameServiceVersion_before.sh
 
content=$1
echo $content
 
salt 'Func' cp.get_dir salt://$content/service/AccountInventoryDaemon 'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/AchievementDaemon      'D:\Service'
wait
 
salt 'Func' cp.get_dir salt://$content/service/AdminWeb               'D:\Service'
salt 'Func' cp.get_dir salt://$content/service/AdminWeb_Txx           'D:\Service'
salt 'Func' cmd.run 'robocopy D:\Service\AdminWeb_Txx D:\Service\AdminWeb /e /np /nfl /ndl'
salt 'Func' cmd.run 'rmdir /s /q D:\Service\AdminWeb_Txx'
 
 
salt 'Func' cp.get_dir salt://$content/service/ArenaLobby             'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/CacheGate              'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/CraftDaemon            'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/DuelbotDaemon          'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/InfoGateDaemon         'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/LobbyDaemon            'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/LobbyGate              'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/ManagementAgent        'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/ManagementDaemon       'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/ManagementWeb          'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/MarketDealerAgent      'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/MarketDealerDaemon     'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/MarketReaderAgent      'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/MarketReaderDaemon     'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/PostOfficeDaemon       'D:\Service' & \
salt 'Func' cp.get_dir salt://$content/service/RankingDaemon          'D:\Service'
wait
 
salt 'Game0*' cp.get_dir salt://$content/service/ArenaDaemon          'D:\Service' & \
salt 'Game0*' cp.get_dir salt://$content/service/CacheDaemon          'D:\Service' & \
salt 'Game0*' cp.get_dir salt://$content/service/GameDaemon           'D:\Service' & \
salt 'Game0*' cp.get_dir salt://$content/service/ManagementAgent      'D:\Service'
wait
 
salt 'Game01' cmd.run 'robocopy D:\Service\ArenaDaemon D:\Service\ArenaDaemon01 /e /np /nfl /ndl'  & \
salt 'Game01' cmd.run 'robocopy D:\Service\CacheDaemon D:\Service\CacheDaemon01 /e /np /nfl /ndl'  & \
salt 'Game01' cmd.run 'robocopy D:\Service\GameDaemon D:\Service\GameDaemon01 /e /np /nfl /ndl'    & \
salt 'Game02' cmd.run 'robocopy D:\Service\ArenaDaemon D:\Service\ArenaDaemon02 /e /np /nfl /ndl'  & \
salt 'Game02' cmd.run 'robocopy D:\Service\CacheDaemon D:\Service\CacheDaemon02 /e /np /nfl /ndl'  & \
salt 'Game02' cmd.run 'robocopy D:\Service\GameDaemon D:\Service\GameDaemon02 /e /np /nfl /ndl'  
wait
 
salt 'Game0*' cmd.run 'rmdir /s /q D:\Service\ArenaDaemon' & \
salt 'Game0*' cmd.run 'rmdir /s /q D:\Service\CacheDaemon' & \
salt 'Game0*' cmd.run 'rmdir /s /q D:\Service\GameDaemon'
wait
 
/srv/salt/QA_script/GameServiceVersion/GameServiceVersion_after.sh
```

