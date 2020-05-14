# How_To_add_windows_update_to_WindowsImage
expain how to add windows update to windows image

If you work in environment you cant access internet,
and you need to update new windows os.

you  take windows iso in that envionment,but iso maybe have bug without installing windows update.

then, you directly add windows update to windows iso!

how to
via powershell,
```
$ mount-diskimage windows.iso
```
iso is immutable,therefor you copy this iso and
modify copied file.
```
$ New-item  expandiso -ItemType Directory
$ Copy-item -recurse -path X:¥ -destination expandiso
```
install.wim is windows image. this file cntent of windows system file and, windows edision info.
take a look, windows image info
```
$ get-windowsimage install.wim
```
each index has different windows image info,and different file system.
because you use all edition,you add windows update to all editions.

```
$ New-item offline -itemType Directory
$ Mount-Windowsimage install.wim -sourceindex 
```

```
$ Add-windowspackage -packagepath
```
take a long time

```
$ get-windowspackage -packagename -path 
```

you look this windows image is added windows update!

```
$ Dismount-Windowsimage -save
```

if offline remain,you dont delete these file how to ordinaly execute command.
you should execute this command.

```
$ clear-windowscorruptmountpoint
```

finaly, you create iso file from expandiso
but, powershell doesnt have cmdlet to create iso file.

windows adk


iso instajled in and, you want to check windows update is exactly installed windows system.

get-hotfix
