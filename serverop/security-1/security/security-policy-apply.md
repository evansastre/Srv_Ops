# Security policy apply

### Security Setting Reg Path <a id="Securitypolicyapply-SecuritySettingRegPath"></a>

Find all key , type , path here , they guide to to the real path, not edit here:

```text
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SeCEdit\Reg Values
```



### Export policy from  template server <a id="Securitypolicyapply-Exportpolicyfromtemplateserver"></a>

1.

```bash
secedit /export /cfg <Path to the exported.inf>
```

2.Edit  policy , left policy what you want to change, other should be delete.

But remenber keep \[Unicode\] \[System Access\] ... these titles.

Keep \[Version\] signature="$CHICAGO$"

3.import

```bash
SECEDIT /configure /db secedit.sdb /cfg <Path to the exported.inf>
```

4.Update group policy

```bash
gpupdate /force
```





Tips: Using salt to deploy security options:

1. Please back up old security setting to C:\ in case of roll back cases.
2. By using salt to run 

```bash
salt 'Target' cmd.run 'echo y | secedit /import /db C:\sec.sdb /cfg C:\sec.inf /overwrite'
```

