**The challenge reads**
```
I am good at maths and english.
```
Download the file,unzip it.we get a .raw file.

# Volatility
I used volatility to solve this challenge.
## imageinfo

>./volatility -f /location of the memory dump/ imageinfo

```
Volatility Foundation Volatility Framework 2.6
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : Win7SP1x64, Win7SP0x64, Win2008R2SP0x64, Win2008R2SP1x64_23418, Win2008R2SP1x64, Win7SP1x64_23418
                     AS Layer1 : WindowsAMD64PagedMemory (Kernel AS)
                     AS Layer2 : FileAddressSpace (/opt/memory.raw)
                      PAE type : No PAE
                           DTB : 0x187000L
                          KDBG : 0xf80002c460a0L
          Number of Processors : 1
     Image Type (Service Pack) : 1
                KPCR for CPU 0 : 0xfffff80002c47d00L
             KUSER_SHARED_DATA : 0xfffff78000000000L
           Image date and time : 2021-08-26 09:53:52 UTC+0000
     Image local date and time : 2021-08-26 14:23:52 +0430
```
we can come to a possible notion that the profile is Win7SP1x64.
## pslist
```
Volatility Foundation Volatility Framework 2.6
Offset(V)          Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start                          Exit                          
------------------ -------------------- ------ ------ ------ -------- ------ ------ ------------------------------ ------------------------------
0xfffffa80018b39e0 System                    4      0     93      391 ------      0 2021-08-26 09:52:16 UTC+0000                                 
0xfffffa8002764b30 smss.exe                260      4      2       29 ------      0 2021-08-26 09:52:16 UTC+0000                                 
0xfffffa800359a590 csrss.exe               348    336      8      511      0      0 2021-08-26 09:52:16 UTC+0000                                 
0xfffffa80037be5f0 wininit.exe             400    336      4       76      0      0 2021-08-26 09:52:17 UTC+0000                                 
0xfffffa8002eb5930 csrss.exe               408    392     10      326      1      0 2021-08-26 09:52:17 UTC+0000                                 
0xfffffa80037f0060 winlogon.exe            456    392      5      113      1      0 2021-08-26 09:52:17 UTC+0000                                 
0xfffffa80037efb30 services.exe            500    400      8      215      0      0 2021-08-26 09:52:17 UTC+0000                                 
0xfffffa8003818b30 lsass.exe               508    400      7      578      0      0 2021-08-26 09:52:17 UTC+0000                                 
0xfffffa8003828b30 lsm.exe                 516    400     10      146      0      0 2021-08-26 09:52:17 UTC+0000                                 
0xfffffa8003866510 svchost.exe             620    500     12      360      0      0 2021-08-26 09:52:17 UTC+0000                                 
0xfffffa80038d7060 vmacthlp.exe            684    500      4       54      0      0 2021-08-26 09:52:17 UTC+0000                                 
0xfffffa80038e2b30 svchost.exe             716    500      7      285      0      0 2021-08-26 09:52:17 UTC+0000                                 
0xfffffa80039154d0 svchost.exe             768    500     19      398      0      0 2021-08-26 09:52:17 UTC+0000                                 
0xfffffa800389c730 svchost.exe             880    500     19      366      0      0 2021-08-26 09:52:17 UTC+0000                                 
0xfffffa800394db30 svchost.exe             928    500     39      942      0      0 2021-08-26 09:52:17 UTC+0000                                 
0xfffffa80039b3b30 audiodg.exe             992    768      6      129      0      0 2021-08-26 09:52:17 UTC+0000                                 
0xfffffa80039f4630 svchost.exe             356    500     14      560      0      0 2021-08-26 09:52:17 UTC+0000                                 
0xfffffa80039ffb30 svchost.exe             832    500     17      382      0      0 2021-08-26 09:52:18 UTC+0000                                 
0xfffffa8003a88060 spoolsv.exe            1108    500     14      302      0      0 2021-08-26 09:52:18 UTC+0000                                 
0xfffffa8003a93b30 taskeng.exe            1116    928      5       81      0      0 2021-08-26 09:52:18 UTC+0000                                 
0xfffffa8003aa0b30 svchost.exe            1152    500     21      318      0      0 2021-08-26 09:52:18 UTC+0000                                 
0xfffffa8003af8b30 armsvc.exe             1252    500      5       63      0      1 2021-08-26 09:52:18 UTC+0000                                 
0xfffffa8003b837c0 VGAuthService.         1352    500      3       87      0      0 2021-08-26 09:52:18 UTC+0000                                 
0xfffffa8003b2f9e0 vmtoolsd.exe           1388    500      9      313      0      0 2021-08-26 09:52:18 UTC+0000                                 
0xfffffa8003c7a630 svchost.exe            1680    500      5      102      0      0 2021-08-26 09:52:19 UTC+0000                                 
0xfffffa8003b8eb30 dllhost.exe            1724    500     20      199      0      0 2021-08-26 09:52:19 UTC+0000                                 
0xfffffa8003c95b30 WmiPrvSE.exe           1736    620     10      187      0      0 2021-08-26 09:52:19 UTC+0000                                 
0xfffffa8003caf510 dllhost.exe            1880    500     17      207      0      0 2021-08-26 09:52:19 UTC+0000                                 
0xfffffa8002abf060 msdtc.exe              2028    500     15      153      0      0 2021-08-26 09:52:22 UTC+0000                                 
0xfffffa8003d29060 VSSVC.exe              1052    500      6      115      0      0 2021-08-26 09:52:22 UTC+0000                                 
0xfffffa8003d76060 taskhost.exe            200    500      9      154      1      0 2021-08-26 09:52:24 UTC+0000                                 
0xfffffa8003daba50 sppsvc.exe             2112    500      5      149      0      0 2021-08-26 09:52:24 UTC+0000                                 
0xfffffa8003de4b30 GoogleCrashHan         2224   2200      6      101      0      1 2021-08-26 09:52:24 UTC+0000                                 
0xfffffa8003df34f0 GoogleCrashHan         2232   2200      6       94      0      0 2021-08-26 09:52:24 UTC+0000                                 
0xfffffa800391cb30 dwm.exe                2416    880      7      129      1      0 2021-08-26 09:52:28 UTC+0000                                 
0xfffffa8003e1cb30 explorer.exe           2428   2408     41      888      1      0 2021-08-26 09:52:28 UTC+0000                                 
0xfffffa8003ecf560 vmtoolsd.exe           2540   2428      9      193      1      0 2021-08-26 09:52:30 UTC+0000                                 
0xfffffa8003836b30 jusched.exe            2600   2548      1       49      1      1 2021-08-26 09:52:30 UTC+0000                                 
0xfffffa80037e2b30 SearchIndexer.         2812    500     15      789      0      0 2021-08-26 09:52:35 UTC+0000                                 
0xfffffa8004059750 AcroRd32.exe           2160   3052     20      474      1      1 2021-08-26 09:52:38 UTC+0000                                 
0xfffffa8004032910 AcroRd32.exe           2212   2160     13      267      1      1 2021-08-26 09:52:38 UTC+0000                                 
0xfffffa80040a4b30 WmiPrvSE.exe            840    620     13      308      0      0 2021-08-26 09:52:39 UTC+0000                                 
0xfffffa800d3ff530 WmiApSrv.exe           2336    500      6      116      0      0 2021-08-26 09:52:40 UTC+0000                                 
0xfffffa80041209e0 dllhost.exe            1300    620      8      222      1      0 2021-08-26 09:52:41 UTC+0000                                 
0xfffffa800413cb30 RdrCEF.exe             2688   2160     30      489      1      1 2021-08-26 09:52:41 UTC+0000                                 
0xfffffa80041f2a80 svchost.exe            2612    500     12      152      0      0 2021-08-26 09:52:41 UTC+0000                                 
0xfffffa8004227060 RdrCEF.exe             2932   2688     13      210      1      1 2021-08-26 09:52:42 UTC+0000                                 
0xfffffa8004292b30 RdrCEF.exe             2556   2688     12      219      1      1 2021-08-26 09:52:43 UTC+0000                                 
0xfffffa800424eb30 RdrCEF.exe             3124   2688     11      200      1      1 2021-08-26 09:52:51 UTC+0000                                 
0xfffffa8002865b30 cmd.exe                3920   1388      0 --------      0      0 2021-08-26 09:53:52 UTC+0000   2021-08-26 09:53:52 UTC+0000  
0xfffffa8002d87330 conhost.exe            3928    348      0 --------      0      0 2021-08-26 09:53:52 UTC+0000   2021-08-26 09:53:52 UTC+0000  
0xfffffa800d574380 ipconfig.exe           3940   3920      0 --------      0      0 2021-08-26 09:53:52 UTC+0000   2021-08-26 09:53:52 UTC+0000 
```
we can see there are some interesting processes running (AcroRd32.exe,RdrCEF.exe).

## cmdline

I can't find any info that peeked my interest when the plugins cmdscan and consoles are used,here is what command line plugin gave.
```
Volatility Foundation Volatility Framework 2.6
************************************************************************
System pid:      4
************************************************************************
smss.exe pid:    260
Command line : \SystemRoot\System32\smss.exe
************************************************************************
csrss.exe pid:    348
Command line : %SystemRoot%\system32\csrss.exe ObjectDirectory=\Windows SharedSection=1024,20480,768 Windows=On SubSystemType=Windows ServerDll=basesrv,1 ServerDll=winsrv:UserServerDllInitialization,3 ServerDll=winsrv:ConServerDllInitialization,2 ServerDll=sxssrv,4 ProfileControl=Off MaxRequestThreads=16
************************************************************************
wininit.exe pid:    400
Command line : wininit.exe
************************************************************************
csrss.exe pid:    408
Command line : %SystemRoot%\system32\csrss.exe ObjectDirectory=\Windows SharedSection=1024,20480,768 Windows=On SubSystemType=Windows ServerDll=basesrv,1 ServerDll=winsrv:UserServerDllInitialization,3 ServerDll=winsrv:ConServerDllInitialization,2 ServerDll=sxssrv,4 ProfileControl=Off MaxRequestThreads=16
************************************************************************
winlogon.exe pid:    456
Command line : winlogon.exe
************************************************************************
services.exe pid:    500
Command line : C:\Windows\system32\services.exe
************************************************************************
lsass.exe pid:    508
Command line : C:\Windows\system32\lsass.exe
************************************************************************
lsm.exe pid:    516
Command line : C:\Windows\system32\lsm.exe
************************************************************************
svchost.exe pid:    620
Command line : C:\Windows\system32\svchost.exe -k DcomLaunch
************************************************************************
vmacthlp.exe pid:    684
Command line : "C:\Program Files\VMware\VMware Tools\vmacthlp.exe"
************************************************************************
svchost.exe pid:    716
Command line : C:\Windows\system32\svchost.exe -k RPCSS
************************************************************************
svchost.exe pid:    768
Command line : C:\Windows\System32\svchost.exe -k LocalServiceNetworkRestricted
************************************************************************
svchost.exe pid:    880
Command line : C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted
************************************************************************
svchost.exe pid:    928
Command line : C:\Windows\system32\svchost.exe -k netsvcs
************************************************************************
audiodg.exe pid:    992
Command line : C:\Windows\system32\AUDIODG.EXE 0x2c4
************************************************************************
svchost.exe pid:    356
Command line : C:\Windows\system32\svchost.exe -k LocalService
************************************************************************
svchost.exe pid:    832
Command line : C:\Windows\system32\svchost.exe -k NetworkService
************************************************************************
spoolsv.exe pid:   1108
Command line : C:\Windows\System32\spoolsv.exe
************************************************************************
taskeng.exe pid:   1116
Command line : taskeng.exe {1BF9FA23-3115-42A2-8F8C-AC5E2C9EB4CA}
************************************************************************
svchost.exe pid:   1152
Command line : C:\Windows\system32\svchost.exe -k LocalServiceNoNetwork
************************************************************************
armsvc.exe pid:   1252
Command line : "C:\Program Files (x86)\Common Files\Adobe\ARM\1.0\armsvc.exe"
************************************************************************
VGAuthService. pid:   1352
Command line : "C:\Program Files\VMware\VMware Tools\VMware VGAuth\VGAuthService.exe"
************************************************************************
vmtoolsd.exe pid:   1388
Command line : "C:\Program Files\VMware\VMware Tools\vmtoolsd.exe"
************************************************************************
svchost.exe pid:   1680
Command line : C:\Windows\system32\svchost.exe -k NetworkServiceNetworkRestricted
************************************************************************
dllhost.exe pid:   1724
Command line : C:\Windows\system32\dllhost.exe /Processid:{941E31E8-68A9-4E77-927C-C8F6DFF550CC}
************************************************************************
WmiPrvSE.exe pid:   1736
Command line : C:\Windows\system32\wbem\wmiprvse.exe
************************************************************************
dllhost.exe pid:   1880
Command line : C:\Windows\system32\dllhost.exe /Processid:{02D4B3F1-FD88-11D1-960D-00805FC79235}
************************************************************************
msdtc.exe pid:   2028
Command line : C:\Windows\System32\msdtc.exe
************************************************************************
VSSVC.exe pid:   1052
Command line : C:\Windows\system32\vssvc.exe
************************************************************************
taskhost.exe pid:    200
Command line : "taskhost.exe"
************************************************************************
sppsvc.exe pid:   2112
Command line : C:\Windows\system32\sppsvc.exe
************************************************************************
GoogleCrashHan pid:   2224
Command line : "C:\Program Files (x86)\Google\Update\1.3.36.102\GoogleCrashHandler.exe"
************************************************************************
GoogleCrashHan pid:   2232
Command line : "C:\Program Files (x86)\Google\Update\1.3.36.102\GoogleCrashHandler64.exe"
************************************************************************
dwm.exe pid:   2416
Command line : "C:\Windows\system32\Dwm.exe"
************************************************************************
explorer.exe pid:   2428
Command line : C:\Windows\Explorer.EXE
************************************************************************
vmtoolsd.exe pid:   2540
Command line : "C:\Program Files\VMware\VMware Tools\vmtoolsd.exe" -n vmusr
************************************************************************
jusched.exe pid:   2600
Command line : "C:\Program Files (x86)\Common Files\Java\Java Update\jusched.exe" 
************************************************************************
SearchIndexer. pid:   2812
Command line : C:\Windows\system32\SearchIndexer.exe /Embedding
************************************************************************
AcroRd32.exe pid:   2160
Command line : "C:\Program Files (x86)\Adobe\Acrobat Reader DC\Reader\AcroRd32.exe" "C:\Program Files\Comonn Files\Systam\en-US\log5413741"
************************************************************************
AcroRd32.exe pid:   2212
Command line : "C:\Program Files (x86)\Adobe\Acrobat Reader DC\Reader\AcroRd32.exe" --type=renderer  "C:\Program Files\Comonn Files\Systam\en-US\log5413741"
************************************************************************
WmiPrvSE.exe pid:    840
Command line : C:\Windows\system32\wbem\wmiprvse.exe
************************************************************************
WmiApSrv.exe pid:   2336
Command line : C:\Windows\system32\wbem\WmiApSrv.exe
************************************************************************
dllhost.exe pid:   1300
Command line : C:\Windows\system32\DllHost.exe /Processid:{76D0CB12-7604-4048-B83C-1005C7DDC503}
************************************************************************
RdrCEF.exe pid:   2688
Command line : "C:\Program Files (x86)\Adobe\Acrobat Reader DC\Reader\AcroCEF\RdrCEF.exe" --backgroundcolor=16514043
************************************************************************
svchost.exe pid:   2612
Command line : C:\Windows\system32\svchost.exe -k LocalServiceAndNoImpersonation
************************************************************************
RdrCEF.exe pid:   2932
Command line : 
************************************************************************
RdrCEF.exe pid:   2556
Command line : 
************************************************************************
RdrCEF.exe pid:   3124
Command line : 
************************************************************************
cmd.exe pid:   3920
************************************************************************
conhost.exe pid:   3928
************************************************************************
ipconfig.exe pid:   3940
```
well,the words that we find in the absolute path of files such as system and common are misspelled on purpose(same says the hint!)

after seeing the output of cmdline I went on and used screenshot ans clipboard plugins.

## screenshot
>./volatility -f /opt/memory.raw --profile=Win7SP1x64 screenshot -D /opt/dump

I stored the results(possible image files) in a directory named dump.

After seeing those images,I got a hit about what I need to find.
![](/images/screenshot.png)

we probably have an image named I'm here.

## clipboard
The output of clipboard plugin gives off something that may be juicy.
```
Volatility Foundation Volatility Framework 2.6
Session    WindowStation Format                         Handle Object             Data                                              
---------- ------------- ------------------ ------------------ ------------------ --------------------------------------------------
         1 WinSta0       0xc009L                       0x702c3 0xfffff900c1e88260                                                   
         1 WinSta0       CF_TEXT                  0x7400000001 ------------------                                                   
         1 WinSta0       CF_UNICODETEXT                0xb0203 0xfffff900c2b03b70 C:\Progrom Files\Comonn ...\en-US\You found me.pdf
         1 WinSta0       CF_TEXT                           0x0 ------------------                                                   
         1 WinSta0       0xc013L                       0x40155 0xfffff900c2b47660                                                   
         1 WinSta0       CF_TEXT                           0x1 ------------------                                                   
         1 ------------- ------------------            0x802bb 0xfffff900c1e05410 
```
This indicates we might probably have a pdf file named You found me(this may not be the case,this so called pdf file hadn't appeared in filescan).So,let's find out.

## filescan
searching for the earlier mentioned I'm here file....
>./volatility -f /opt/memory.raw --profile=Win7SP1x64 filescan | grep -i here

```
0x000000007d71b1d0      2      0 R--r-d \Device\HarddiskVolume1\Users\I'm hidden.WIN-VJ4BGD4ID7K\Downloads\I'm here.png
```
let's dump this using the command
>./volatility -f /opt/memory.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000007d71b1d0 -D /opt/dump/

we find a QR code ,which after scanning gives us a string which looks like the second part of the flag,
**OD_iN_ch3mI$7ry}**

I used filescan plugin with no filters this time to see the output.

## dlllist

Travelling back to the pslist plugin's output,note down the process ID of AcroRd32.exe,let's dump dll's in both the process.

>./volatility -f /opt/memory.raw --profile=Win7SP1x64 dlllist -p 2160,2212
```
AcroRd32.exe pid:   2160
Command line : "C:\Program Files (x86)\Adobe\Acrobat Reader DC\Reader\AcroRd32.exe" "C:\Program Files\Comonn Files\Systam\en-US\log5413741"
Note: use ldrmodules for listing DLLs in Wow64 processes


Base                             Size          LoadCount Path
------------------ ------------------ ------------------ ----
0x0000000001310000           0x308000             0xffff C:\Program Files (x86)\Adobe\Acrobat Reader DC\Reader\AcroRd32.exe
0x0000000077860000           0x1a9000             0xffff C:\Windows\SYSTEM32\ntdll.dll
0x0000000074040000            0x3f000                0x3 C:\Windows\SYSTEM32\wow64.dll
0x0000000073fe0000            0x5c000                0x1 C:\Windows\SYSTEM32\wow64win.dll
0x0000000073fd0000             0x8000                0x1 C:\Windows\SYSTEM32\wow64cpu.dll
************************************************************************
AcroRd32.exe pid:   2212
Command line : "C:\Program Files (x86)\Adobe\Acrobat Reader DC\Reader\AcroRd32.exe" --type=renderer  "C:\Program Files\Comonn Files\Systam\en-US\log5413741"
Note: use ldrmodules for listing DLLs in Wow64 processes


Base                             Size          LoadCount Path
------------------ ------------------ ------------------ ----
0x0000000001310000           0x308000             0xffff C:\Program Files (x86)\Adobe\Acrobat Reader DC\Reader\AcroRd32.exe
0x0000000077860000           0x1a9000             0xffff C:\Windows\SYSTEM32\ntdll.dll
0x0000000074040000            0x3f000                0x3 C:\Windows\SYSTEM32\wow64.dll
0x0000000073fe0000            0x5c000                0x1 C:\Windows\SYSTEM32\wow64win.dll
0x0000000073fd0000             0x8000                0x1 C:\Windows\SYSTEM32\wow64cpu.dll
```
let's dump the log5413741 file.(get the virtual memory address of this file from filescan 0x000000007d681aa0)
>./volatility -f /opt/memory.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000007d681aa0  -D /opt/dump/

use the file command or open the dump directory(or whereever the file is in a file viewer),its a pdf file :)

opening the pdf  file we find the following link,
https://tinyurl.com/t7zpyfb6
which leads us to a mega file.I downloaded the so called You found me again.png image file.

There's a problem with the png file header,I changed it using a hexeditor and opened the png file to get our flag.
![](/images/flag-part-1.png)

**TMUCTF{M@Y8e_1_@M_6oOD_iN_ch3mI$7ry}**



