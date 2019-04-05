# PreServer\_Patch

```text
##/srv/salt/live_script/PreServer_Patch_live.sh

NewServerPatch=$1
#NewServerPatch='$new_server_patch'
echo $NewServerPatchs
 
cd/home/release
rm -rf /srv/salt/newserverpatch
mkdir -p newserverpatch
 
 
NewServerPatch_arr={$NewServerPatchs}
for NewServerPatch in ${NewServerPatch_arr[@]; do
{
 
 
    echo $NewServerPatch
    rm -rf '/home/release/'$NewServerPatch
    sudo /usr/local/bin/unrar x -o+ '/home/release/'$NewServerPatch.rar /home/release
    if [[ ! -d '/home/release/'$NewServerPatch ]]; then
        echo "Pls check the package name!!!"
        exit 1
    fi 
    mv 'home/release'$NewServerPatch'Service' '/home/release/'$NewServerPatch'/service'
    sudo rsync -av '/home/release/'$NewServerPatch'/'  /home/release/newserverpatch
 
}

done
sudo mv /home/release/newserverpatch /srv/salt
 
bash /srv/salt/LIVE_Script/Server_Patch_LIVE.sh newserverpatch
 
```

