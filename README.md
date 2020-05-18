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
$ Copy-item -recurse -path X:¥ -destination expandiso
```
install.wim is windows image. this file cntent of windows system file and, windows edision info.
take a look, windows image info
```
$ Get-windowsimage -ImagePath .¥expandiso¥sources¥install.wim
```

each index has different windows image info,and different file system.
because you use all edition,you add windows update to all editions.

If you need to take a look at Windows Image contents files, you execute this command.
```
$ $indexnum = 1
$ Get-WindowsImageContent -ImagePath .¥expandiso¥sources¥install.wim -Index $indexnum
```
indexnum is index number you want to know Windows Edition has.

```
$ New-item offline -itemType Directory
$ Mount-Windowsimage -ImagePath .¥expandiso¥sources¥install.wim -path .¥offline -sourceindex $indexnum
```

```
$ Add-windowspackage -path .¥offline -packagepath
```
take a long time

```
$ get-windowspackage -path .¥offline
```

you look this windows image is added windows update!

```
$ Dismount-Windowsimage -path .¥offline -save
```

if offline remain,you dont delete these file how to ordinaly execute command.
you should execute this command.

```
$ clear-windowscorruptmountpoint
```

finaly, you create iso file from expandiso
but, powershell doesnt have cmdlet to create iso file.

you need to download windows adk from Microsoft officiail and install it.

```
C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools\amd64\Oscdimg\oscdimg.exe
```

```
$ $Env:Path = $Env:Path + "C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools\amd64\Oscdimg;"
```


iso instajled in and, you want to check windows update is exactly installed windows system.

get-hotfix
