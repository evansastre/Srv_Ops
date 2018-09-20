# Apply Server Patch For LIVE

```bash
#!/bin/bash

content=$1
echo $content

####Functions
salt 'AccountIn' cp.get_dir salt://$content/service/AccountInventoryDaemon   'D:\Service' & \
salt 'Achieve'   cp.get_dir salt://$content/service/AchievementDaemon 	     'D:\Service'
wait 

#AdminWeb mention:AdminWeb_TH,AdminWeb_VN
salt 'AdminWeb'  cp.get_dir salt://$content/service/AdminWeb        	     'D:\Service'
salt 'AdminWeb'  cp.get_dir salt://$content/service/AdminWeb_Txx             'D:\Service'
salt 'AdminWeb'  cmd.run 'robocopy D:\Service\AdminWeb_Txx D:\Service\AdminWeb /e /np /nfl /ndl'
salt 'AdminWeb'  cmd.run 'rmdir /s /q D:\Service\AdminWeb_Txx'

salt 'ArenaLB'   cp.get_dir salt://$content/service/ArenaLobby			     'D:\Service' & \
salt 'CacheGate' cp.get_dir salt://$content/service/CacheGate			     'D:\Service' & \
#salt 'CraftD'    cp.get_dir salt://$content/service/CraftDaemon		     'D:\Service' & \
salt 'DuelBot'   cp.get_dir salt://$content/service/DuelbotDaemon		     'D:\Service' & \
salt 'InGateD0*' cp.get_dir salt://$content/service/InfoGateDaemon 	         'D:\Service' & \
salt 'LobbyD'    cp.get_dir salt://$content/service/LobbyDaemon		         'D:\Service' & \
salt 'LoGateD0*' cp.get_dir salt://$content/service/LobbyGate			     'D:\Service' & \
salt -N 'Management' cp.get_dir salt://$content/service/ManagementAgent	 	 'D:\Service' & \
salt 'AdminWeb' cp.get_dir salt://$content/service/ManagementDaemon	  	 	 'D:\Service' & \
salt 'AdminWeb' cp.get_dir salt://$content/service/ManagementWeb		   	 'D:\Service' & \
salt 'MarkDARA' cp.get_dir salt://$content/service/MarketDealerAgent	  	 'D:\Service' & \
salt 'MarketDD' cp.get_dir salt://$content/service/MarketDealerDaemon	 	 'D:\Service' & \
salt 'MarkDARA' cp.get_dir salt://$content/service/MarketReaderAgent	   	 'D:\Service' & \
salt 'MarketRD' cp.get_dir salt://$content/service/MarketReaderDaemon	   	 'D:\Service' & \
salt 'PostOffD' cp.get_dir salt://$content/service/PostOfficeDaemon 	   	 'D:\Service' & \
salt 'Rank'	  cp.get_dir salt://$content/service/RankingDaemon		   	 	 'D:\Service'
wait

####Game
salt 'ArenaD0*'  cp.get_dir salt://$content/service/ArenaDaemon	   		 'D:\Service' & \
salt 'Dungeon0*' cp.get_dir salt://$content/service/ArenaDaemon	   		 'D:\Service' & \
salt 'WorldDB*'  cp.get_dir salt://$content/service/CacheDaemon	   		 'D:\Service' & \
salt -N 'World'  cp.get_dir salt://$content/service/GameDaemon		     'D:\Service'

```

