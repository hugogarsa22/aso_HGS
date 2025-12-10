# PR0602: El pipeline en Powershell

Realiza las siguientes tareas que se te piden utilizando **Powershell**. Para contestar lo mejor es que hagas una captura de pantalla donde se vea el comando que has introducido y las primeras líneas de la salida de este.

1. El comando `Get-Date` muestra la fecha y hora actual. Muestra por pantalla únicamente el año en que estamos.
``` bash
PS C:\WINDOWS\system32> Get-Date -Format "yyyy"
2025
```
2. Uno de los requisitos de Windows 11 es que es procesador tenga **TPM** habilitado. Powershell dispone del comando `Get-TPM` que nos muestra información sobre este módulo. Muestra por pantalla, en formato tabla, las propiedades `TpmPresent`, `TpmReady`, `TpmEnabled` y `TpmActivated`.

```bash
PS C:\Windows\system32> Get-TPM | Format-Table TpmPresent, TpmReady, TpmEnabled, TpmActivated

TpmPresent TpmReady TpmEnabled TpmActivated
---------- -------- ---------- ------------
      True     True       True         True

```
En los siguientes ejercicios trabajaremos con los ficheros devueltos por el comando `Get-ChildItem C:\Windows\System32`.

3. Muestra por pantalla el número de ficheros y directorios que hay en ese directorio.
```bash
PS C:\WINDOWS\system32> Get-ChildItem  | Measure-Object


Count    : 4960
Average  :
Sum      :
Maximum  :
Minimum  :
Property :
```
4. Los objetos devueltos por el comando anterior tienen una propiedad denominada `Extension`, que indica la extensión del archivo. Calcula el número de ficheros en el directorio que tienen la extensión `.dll`.
```bash
PS C:\WINDOWS\system32> Get-ChildItem | Where-Object {$_.Extension -eq ".dll"} | Measure-Object


Count    : 3631
Average  :
Sum      :
Maximum  :
Minimum  :
Property :
```

5. Muestra los ficheros del directorio con extensión `.exe` que tengan un tamaño superior a 50000 bytes.

```bash
PS C:\Windows\system32> Get-ChildItem | Where-Object { $_.Extension -eq ".exe" -and $_.Length -gt 50000 }


    Directorio: C:\Windows\system32


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        13/06/2025      2:03        1220608 AgentService.exe
-a----        17/05/2025      2:16         328192 AggregatorHost.exe
-a----        04/10/2025      2:04        3262464 aitstatic.exe
-a----        04/12/2023      3:46          95744 alg.exe
-a----        27/10/2025     17:23         471480 amdlogum.exe
-a----        21/02/2025     18:47         120320 AppHostRegistrationVerifier.exe
-a----        17/05/2025      2:16          50176 appidcertstorecheck.exe
-a----        04/12/2023      3:46         160768 appidpolicyconverter.exe
-a----        17/05/2025      2:16          80120 ApplicationFrameHost.exe
-a----        17/05/2025      2:17        1157120 ApplySettingsTemplateCatalog.exe
-a----        18/10/2025      2:05        1224672 ApplyTrustOffline.exe
-a----        21/02/2025     18:47         235008 ApproveChildRequest.exe
-a----        17/05/2025      2:17         777152 AppVClient.exe
-a----        21/02/2025     18:48         177136 AppVDllSurrogate.exe
-a----        21/02/2025     18:48         168304 AppVNice.exe
-a----        21/02/2025     18:48         221056 AppVShNotify.exe
-a----        21/02/2025     18:48         103936 AssignedAccessGuard.exe
-a----        21/02/2025     18:47          92672 AtBroker.exe
-a----        27/10/2025     17:24         559544 atieah64.exe
-a----        27/10/2025     17:24        1068472 atieclxx.exe
-a----        17/05/2025      2:16         632880 audiodg.exe
-a----        04/12/2023      3:46         141136 AuthHost.exe
-a----        04/12/2023      3:46         972800 autochk.exe
-a----        04/12/2023      3:47         947200 autoconv.exe
-a----        04/12/2023      3:47         921088 autofmt.exe
-a----        21/02/2025     18:48          60928 AxInstUI.exe
-a----        07/12/2019     15:58         113152 baaupdate.exe
-a----        18/11/2025     18:29          90112 bash.exe
-a----        21/02/2025     18:47         259584 bcdboot.exe
-a----        21/02/2025     18:47         493576 bcdedit.exe
-a----        14/04/2025      1:41         384512 bdechangepin.exe
-a----        04/12/2023      3:48         134144 BdeHdCfg.exe
-a----        13/06/2025      2:03          55808 BdeUISrv.exe
-a----        04/12/2023      3:48         287840 bdeunlock.exe
-a----        17/05/2025      2:16         744480 BioIso.exe
-a----        17/05/2025      2:17         178688 BitLockerDeviceEncryption.exe
-a----        04/12/2023      3:48         102400 BitLockerWizard.exe
-a----        04/12/2023      3:48         102400 BitLockerWizardElev.exe
-a----        07/12/2019     10:08         211456 bitsadmin.exe
-a----        07/12/2019     10:08          97280 bootcfg.exe
-a----        07/12/2019     10:08         110392 bootsect.exe
-a----        21/02/2025     18:47         140800 browserexport.exe
-a----        21/02/2025     18:47          82944 ByteCodeGenerator.exe
-a----        04/12/2023      3:47          63704 CastSrv.exe
-a----        15/03/2025      1:44          66048 CertEnrollCtrl.exe
-a----        17/05/2025      2:17         594432 certreq.exe
-a----        17/05/2025      2:17        1679872 certutil.exe
-a----        21/02/2025     18:47         103824 changepk.exe
-a----        21/02/2025     18:48         198656 charmap.exe
-a----        13/06/2025      2:03         315904 cleanmgr.exe
-a----        27/10/2025     17:23         347072 clinfo.exe
-a----        18/10/2025      2:05         346496 clipesu.exe
-a----        18/10/2025      2:05         531344 ClipESUConsumer.exe
-a----        17/05/2025      2:15         182200 ClipRenew.exe
-a----        18/10/2025      2:06        1167896 ClipUp.exe
-a----        21/02/2025     18:47          70016 CloudExperienceHostBroker.exe
-a----        21/02/2025     18:47          61496 CloudNotifications.exe
-a----        21/02/2025     18:47         289792 cmd.exe
-a----        07/12/2019     10:09          54784 cmdl32.exe
-a----        07/12/2019     10:09          98304 cmstp.exe
-a----        07/12/2019     10:08          87552 colorcpl.exe
-a----        04/10/2025      2:05         254824 CompatTelRunner.exe
-a----        07/12/2019     10:09          91136 CompMgmtLauncher.exe
-a----        21/02/2025     18:47         215040 CompPkgSrv.exe
-a----        17/05/2025      2:16          81920 ComputerDefaults.exe
-a----        21/02/2025     18:47         867840 conhost.exe
-a----        17/05/2025      2:16         187336 consent.exe
-a----        17/05/2025      2:16         164352 control.exe
-a----        04/10/2025      2:04         230312 convertvhd.exe
-a----        21/02/2025     18:47          50688 coredpussvr.exe
-a----        17/05/2025      2:16         388000 CredentialEnrollmentManager.exe
-a----        21/02/2025     18:47         149344 CredentialUIBroker.exe
-a----        17/05/2025      2:16         173056 cscript.exe
-a----        07/12/2019     10:09          92160 cttune.exe
-a----        04/10/2025      2:05         711736 curl.exe
-a----        04/10/2025      2:05         138752 CustomInstallExec.exe
-a----        18/10/2025      2:06        1266176 CustomShellHost.exe
-a----        04/12/2023      3:46          98816 dasHost.exe
-a----        17/05/2025      2:16         261024 DataExchangeHost.exe
-a----        04/10/2025      2:04         162304 DataStoreCacheDumpTool.exe
-a----        17/05/2025      2:16         176640 DataUsageLiveTileTask.exe
-a----        07/12/2019     10:08         103424 dccw.exe
-a----        04/12/2023      3:47         210432 Defrag.exe
-a----        17/05/2025      2:16          87040 desktopimgdownldr.exe
-a----        17/05/2025      2:16          82944 DeviceCensus.exe
-a----        21/02/2025     18:47          82432 DeviceCredentialDeployment.exe
-a----        04/10/2025      2:05         502784 DeviceEnroller.exe
-a----        21/02/2025     18:48          95744 DevicePairingWizard.exe
-a----        07/12/2019     10:09          94720 DeviceProperties.exe
-a----        07/12/2019     10:09          54784 DFDWiz.exe
-a----        04/12/2023      3:47         119296 dfrgui.exe
-a----        27/10/2025     17:23         549304 dgtrayicon.exe
-a----        17/05/2025      2:16         305664 directxdatabaseupdater.exe
-a----        04/12/2023      3:46         159232 diskpart.exe
-a----        07/12/2019     10:08         338944 diskraid.exe
-a----        04/12/2023      3:46          85504 DiskSnapshot.exe
-a----        04/12/2023      3:46         289136 Dism.exe
-a----        07/12/2019     10:08         121344 dispdiag.exe
-a----        21/02/2025     18:48        1925104 DisplaySwitch.exe
-a----        04/12/2023      3:46          75776 djoin.exe
-a----        17/05/2025      2:16         189952 dmcertinst.exe
-a----        21/02/2025     18:47         120832 dmclient.exe
-a----        07/12/2019     10:09          77824 dpapimig.exe
-a----        07/12/2019     10:09          79360 DpiScaling.exe
-a----        07/12/2019     10:09          87552 driverquery.exe
-a----        17/05/2025      2:16         349696 drvinst.exe
-a----        04/12/2023      3:47         468992 dsregcmd.exe
-a----        21/02/2025     18:47         129032 DTUHandler.exe
-a----        21/02/2025     18:47          94720 dwm.exe
-a----        17/05/2025      2:16         241664 DWWIN.EXE
-a----        07/12/2019     10:09         272384 dxdiag.exe
-a----        17/05/2025      2:16         251392 dxgiadaptercache.exe
-a----        21/02/2025     18:48         317952 Dxpserver.exe
-a----        21/02/2025     18:47         125952 EaseOfAccessDialog.exe
-a----        04/10/2025      2:05          80680 easinvoker.exe
-a----        21/02/2025     18:48          64512 EASPolicyManagerBrokerHost.exe
-a----        17/05/2025      2:16         173568 EDPCleanup.exe
-a----        21/02/2025     18:48          62976 edpnotify.exe
-a----        21/02/2025     18:48         100352 EduPrintProv.exe
-a----        27/10/2025     17:24         526264 EEURestart.exe
-a----        07/12/2019     10:09         131584 EhStorAuthn.exe
-a----        17/05/2025      2:16         673080 EM.exe
-a----        17/05/2025      2:16         152576 EoAExperiences.exe
-a----        07/12/2019     10:09         409600 esentutl.exe
-a----        21/02/2025     18:48         374272 eudcedit.exe
-a----        07/12/2019     10:09          84480 eventvwr.exe
-a----        07/12/2019     10:08          67584 expand.exe
-a----        18/10/2025      2:06         456128 fclip.exe
-a----        04/12/2023      3:47         140800 fhmanagew.exe
-a----        04/12/2023      3:47         249856 FileHistory.exe
-a----        21/02/2025     18:48         113152 Fondue.exe
-a----        17/05/2025      2:16         830056 fontdrvhost.exe
-a----        21/02/2025     18:47         123392 fontview.exe
-a----        07/12/2019     10:09          52224 forfiles.exe
-a----        13/06/2025      2:03         102960 FsIso.exe
-a----        18/10/2025      2:05         171520 fsquirt.exe
-a----        21/02/2025     18:48         215920 fsutil.exe
-a----        07/12/2019     10:09          58880 ftp.exe
-a----        07/12/2019     15:58         174080 fvenotify.exe
-a----        07/12/2019     15:58         161280 fveprompt.exe
-a----        04/10/2025      2:05         248320 FXSCOVER.exe
-a----        04/12/2023      3:48         663552 FXSSVC.exe
-a----        21/02/2025     18:48         337920 GameBarPresenceWriter.exe
-a----        04/10/2025      2:04          55168 GameInputSvc.exe
-a----        17/05/2025      2:16        1267200 GamePanel.exe
-a----        04/12/2023      3:46         674056 GenValObj.exe
-a----        07/12/2019     10:09          90112 getmac.exe
-a----        04/12/2025     18:14          89336 GigabyteDownloadAssistant.exe
-a----        04/12/2025     18:13         878840 GigabyteUpdateService.exe
-a----        17/05/2025      2:16         285184 gpresult.exe
-a----        21/02/2025     18:48          53248 grpconv.exe
-a----        21/02/2025     18:48         261512 hcsdiag.exe
-a----        07/12/2019     10:09          68096 hdwwiz.exe
-a----        17/05/2025      2:17         158208 hnsdiag.exe
-a----        18/10/2025      2:06        1307520 hvax64.exe
-a----        18/10/2025      2:06        1574784 hvix64.exe
-a----        17/05/2025      2:17         161200 hvsievaluator.exe
-a----        13/06/2025      2:03         257024 ie4uinit.exe
-a----        13/06/2025      2:03          96256 ie4ushowIE.exe
-a----        04/10/2025      2:05         545792 IESettingSync.exe
-a----        21/02/2025     18:48         158720 ieUnatt.exe
-a----        07/12/2019     10:09         170496 iexpress.exe
-a----        21/02/2025     18:47         144384 immersivetpmvscmgrsvr.exe
-a----        21/02/2025     18:48          86528 InputSwitchToastHandler.exe
-a----        17/05/2025      2:17         138680 iotstartup.exe
-a----        21/02/2025     18:48          50688 iscsicli.exe
-a----        21/02/2025     18:48         122368 isoburn.exe
-a----        17/05/2025      2:17          76288 klist.exe
-a----        21/02/2025     18:48          52736 LanguageComponentsInstallerComHandler.exe
-a----        17/05/2025      2:16         243712 LegacyNetUXHost.exe
-a----        04/10/2025      2:04         397312 licensingdiag.exe
-a----        04/12/2023      3:46         146816 LicensingUI.exe
-a----        13/06/2025      2:03          89600 LocationNotificationWindows.exe
-a----        17/05/2025      2:16          94128 LockAppHost.exe
-a----        07/12/2019     10:08          52224 lodctr.exe
-a----        04/12/2023      3:47         112640 logagent.exe
-a----        04/12/2023      3:47         120320 logman.exe
-a----        04/10/2025      2:05         745472 lpksetup.exe
-a----        04/10/2025      2:05          97280 lpremove.exe
-a----        18/10/2025      2:05         343024 LsaIso.exe
-a----        04/10/2025      2:05          61072 lsass.exe
-a----        17/05/2025      2:16         650752 Magnify.exe
-a----        04/12/2023      3:46          86528 makecab.exe
-a----        07/12/2019     15:58         227328 manage-bde.exe
-a----        21/02/2025     18:48         183680 mavinject.exe
-a----        07/12/2019     10:09         119296 MbaeParserTask.exe
-a----        21/02/2025     18:48         808960 mblctr.exe
-a----        04/10/2025      2:05        1187840 MBR2GPT.EXE
-a----        07/12/2019     10:08          94208 mcbuilder.exe
-a----        04/12/2023      3:47         454656 MDEServer.exe
-a----        17/05/2025      2:16         168960 MDMAgent.exe
-a----        17/05/2025      2:16         174592 MDMAppInstaller.exe
-a----        21/02/2025     18:47          52736 MdmDiagnosticsTool.exe
-a----        07/12/2019     10:09          87040 MdRes.exe
-a----        07/12/2019     10:09          92672 MdSched.exe
-a----        21/02/2025     18:48         422912 Microsoft.Uev.CscUnpinTool.exe
-a----        07/12/2019     15:58          83456 Microsoft.Uev.SyncController.exe
-a----        21/02/2025     18:47          97280 MicrosoftEdgeBCHost.exe
-a----        21/02/2025     18:48          97280 MicrosoftEdgeCP.exe
-a----        21/02/2025     18:47          97280 MicrosoftEdgeDevTools.exe
-a----        21/02/2025     18:47          58880 MicrosoftEdgeSH.exe
-a----        04/10/2025      2:05        1955328 mmc.exe
-a----        21/02/2025     18:47        1288704 mmgaserver.exe
-a----        21/02/2025     18:48          99328 mobsync.exe
-a----        17/05/2025      2:16        1971200 MoUsoCoreWorker.exe
------        21/02/2025     18:25         918944 MpSigStub.exe
-a----        24/11/2025      2:00      215625816 MRT.exe
-a----        07/12/2019     10:08          83968 MSchedExe.exe
-a----        04/12/2023      3:47         197632 msconfig.exe
-a----        21/02/2025     18:48         498176 msdt.exe
-a----        17/05/2025      2:16         182784 msdtc.exe
-a----        21/02/2025     18:48          69632 msiexec.exe
-a----        04/12/2023      3:47         386048 msinfo32.exe
-a----        15/03/2025      1:45         938496 mspaint.exe
-a----        04/12/2023      3:48         592896 msra.exe
-a----        04/10/2025      2:05         123904 MsSpellCheckingHost.exe
-a----        13/06/2025      2:03        1288704 mstsc.exe
-a----        07/12/2019     10:08         137216 mtstocom.exe
-a----        17/05/2025      2:16         107008 MuiUnattend.exe
-a----        07/12/2019     10:09          54784 MultiDigiMon.exe
-a----        04/10/2025      2:04         697344 MusNotification.exe
-a----        04/10/2025      2:04         633344 MusNotificationUx.exe
-a----        04/10/2025      2:04         649792 MusNotifyIcon.exe
-a----        17/05/2025      2:16         534016 Narrator.exe
-a----        04/10/2025      2:05          69632 ndadmin.exe
-a----        07/12/2019     10:09          59904 net.exe
-a----        04/12/2023      3:47         183808 net1.exe
-a----        21/02/2025     18:48          76288 NetCfgNotifyObjectHost.exe
-a----        07/12/2019     10:09          96768 netsh.exe
-a----        04/10/2025      2:05          72192 newdev.exe
-a----        14/04/2025      1:41         498576 NgcIso.exe
-a----        13/06/2025      2:03         541184 nltest.exe
-a----        21/02/2025     18:48         143856 nmbind.exe
-a----        21/02/2025     18:48         152448 nmscrub.exe
-a----        17/05/2025      2:17         200704 notepad.exe
-a----        07/12/2019     10:08          89600 nslookup.exe
-a----        18/10/2025      2:05       10859424 ntoskrnl.exe
-a----        04/12/2023      3:46          64000 ntprint.exe
-a----        17/05/2025      2:17         292784 nvspinfo.exe
-a----        07/12/2019     10:09          74240 odbcad32.exe
-a----        04/12/2023      3:45          79872 ofdeploy.exe
-a----        04/10/2025      2:05         514560 omadmclient.exe
-a----        04/10/2025      2:05         134144 omadmprc.exe
-a----        21/02/2025     18:47         102832 OOBE-Maintenance.exe
-a----        07/12/2019     10:09          75776 openfiles.exe
-a----        17/05/2025      2:16         126144 OpenWith.exe
-a----        21/02/2025     18:48         112640 OptionalFeatures.exe
-a----        17/05/2025      2:16         674304 osk.exe
-a----        07/12/2019     15:58          90624 PackageInspector.exe
-a----        04/10/2025      2:05          91136 pcalua.exe
-a----        04/10/2025      2:04         222208 pcaui.exe
-a----        07/12/2019     10:09         181760 perfmon.exe
-a----        04/12/2023      3:46         111696 phoneactivate.exe
-a----        17/05/2025      2:16         128168 PickerHost.exe
-a----        17/05/2025      2:16         112128 PinEnrollmentBroker.exe
-a----        17/05/2025      2:16         250880 PkgMgr.exe
-a----        21/02/2025     18:48         682464 PktMon.exe
-a----        04/12/2023      3:46          62976 PnPUnattend.exe
-a----        17/05/2025      2:16         329728 pnputil.exe
-a----        27/09/2025      6:16         498176 poqexec.exe
-a----        07/12/2019     10:09          96256 powercfg.exe
-a----        07/12/2019     10:10         282624 PresentationHost.exe
-a----        21/02/2025     18:48         224768 PresentationSettings.exe
-a----        04/12/2023      3:47          75776 PrintBrmUi.exe
-a----        17/05/2025      2:16         748544 printfilterpipelinesvc.exe
-a----        04/12/2023      3:45          77312 PrintIsolationHost.exe
-a----        04/12/2023      3:46          64000 printui.exe
-a----        17/05/2025      2:16          68096 proquota.exe
-a----        04/10/2025      2:05          62976 provlaunch.exe
-a----        04/10/2025      2:04          87040 provtool.exe
-a----        21/02/2025     18:48         271184 ProximityUxHost.exe
-a----        04/12/2023      3:47         237568 psr.exe
-a----        17/05/2025      2:17         952320 quickassist.exe
-a----        04/12/2023      3:48         135168 raserver.exe
-a----        13/06/2025      2:03         473088 rdpclip.exe
-a----        13/06/2025      2:03         344576 rdpinit.exe
-a----        13/06/2025      2:03         196608 rdpinput.exe
-a----        13/06/2025      2:03          69120 RdpSa.exe
-a----        13/06/2025      2:03          53248 RdpSaProxy.exe
-a----        13/06/2025      2:03         461312 rdpshell.exe
-a----        13/06/2025      2:03         113664 rdpsign.exe
-a----        18/10/2025      2:05          57856 readCloudDataSettings.exe
-a----        17/05/2025      2:17         234496 recdisc.exe
-a----        13/06/2025      2:03         943616 RecoveryDrive.exe
-a----        17/05/2025      2:16        1024000 refsutil.exe
-a----        07/12/2019     10:09          77312 reg.exe
-a----        04/12/2023      3:46         122880 rekeywiz.exe
-a----        04/12/2023      3:47          53760 relog.exe
-a----        13/06/2025      2:03         194048 RelPost.exe
-a----        17/05/2025      2:17          98304 RemoteAppLifetimeManager.exe
-a----        21/02/2025     18:48         129024 repair-bde.exe
-a----        07/12/2019     10:09         110592 resmon.exe
-a----        04/10/2025      2:04         137936 rgnupdt.exe
-a----        04/12/2023      3:45         579584 RMActivate.exe
-a----        04/12/2023      3:45         607744 RMActivate_isv.exe
-a----        04/12/2023      3:45         501760 RMActivate_ssp.exe
-a----        07/12/2019     10:08         501760 RMActivate_ssp_isv.exe
-a----        21/02/2025     18:47         142848 rmttpmvscmgrsvr.exe
-a----        17/05/2025      2:16         172544 Robocopy.exe
-a----        21/02/2025     18:48         274432 rstrui.exe
-a----        17/05/2025      2:16          89600 rundll32.exe
-a----        17/05/2025      2:16          61440 runexehelper.exe
-a----        21/02/2025     18:47          74240 RunLegacyCPLElevated.exe
-a----        21/02/2025     18:48          61952 runonce.exe
-a----        17/05/2025      2:16         102864 RuntimeBroker.exe
-a----        07/12/2019     10:09          72192 sc.exe
-a----        13/06/2025      2:03         268800 schtasks.exe
-a----        04/12/2023      3:48          51712 sdchange.exe
-a----        17/05/2025      2:16        1265152 sdclt.exe
-a----        18/10/2025      2:05         272896 SearchFilterHost.exe
-a----        18/10/2025      2:05         936960 SearchIndexer.exe
-a----        18/10/2025      2:05         419328 SearchProtocolHost.exe
-a----        18/10/2025      2:06         923520 securekernel.exe
-a----        17/05/2025      2:16          99232 SecurityHealthHost.exe
-a----        17/05/2025      2:16         988152 SecurityHealthService.exe
-a----        21/02/2025     18:47          86016 SecurityHealthSystray.exe
-a----        21/02/2025     18:47        1265152 SensorDataService.exe
-a----        17/05/2025      2:16         716480 services.exe
-a----        04/12/2023      3:47          88368 sessionmsg.exe
-a----        21/02/2025     18:47         107008 sethc.exe
-a----        17/05/2025      2:16         970696 SettingSyncHost.exe
-a----        04/12/2023      3:46         137216 setupugc.exe
-a----        07/12/2019     10:09          58368 setx.exe
-a----        07/12/2019     10:08          50176 sfc.exe
-a----        18/10/2025      2:05        1265000 ShellAppRuntime.exe
-a----        07/12/2019     10:09          60928 shrpubw.exe
-a----        07/12/2019     10:09          79360 sigverif.exe
-a----        04/10/2025      2:05         418456 SIHClient.exe
-a----        17/05/2025      2:16         111104 sihost.exe
-a----        18/10/2025      2:05         574976 slui.exe
-a----        18/10/2025      2:05        2380288 smartscreen.exe
-a----        17/05/2025      2:16         175216 smss.exe
-a----        21/02/2025     18:47         276920 SndVol.exe
-a----        17/05/2025      2:17         165888 SpaceAgent.exe
-a----        17/05/2025      2:16          80800 spaceman.exe
-a----        17/05/2025      2:16         152576 SpatialAudioLicenseSrv.exe
-a----        17/05/2025      2:17         878080 Spectrum.exe
-a----        04/10/2025      2:04         847872 spoolsv.exe
-a----        17/05/2025      2:16         572928 SppExtComObj.Exe
-a----        18/10/2025      2:05        4669216 sppsvc.exe
-a----        04/12/2023      3:47          59392 SrTasks.exe
-a----        07/12/2019     10:09         111616 stordiag.exe
-a----        17/05/2025      2:16          57480 svchost.exe
-a----        07/12/2019     10:09         110080 systeminfo.exe
-a----        07/12/2019     10:09          83968 SystemPropertiesAdvanced.exe
-a----        07/12/2019     10:09          83968 SystemPropertiesComputerName.exe
-a----        07/12/2019     10:09          83968 SystemPropertiesDataExecutionPrevention.exe
-a----        07/12/2019     10:09          83968 SystemPropertiesHardware.exe
-a----        07/12/2019     10:09          84480 SystemPropertiesPerformance.exe
-a----        07/12/2019     10:09          83968 SystemPropertiesProtection.exe
-a----        07/12/2019     10:09          83968 SystemPropertiesRemote.exe
-a----        18/10/2025      2:06         522192 systemreset.exe
-a----        04/10/2025      2:04         522272 SystemSettingsAdminFlows.exe
-a----        18/10/2025      2:05         206144 SystemSettingsBroker.exe
-a----        21/02/2025     18:47          86016 SystemUWPLauncher.exe
-a----        07/12/2019     10:09          86016 tabcal.exe
-a----        07/12/2019     10:09          66560 takeown.exe
-a----        04/12/2023      3:47          54784 tar.exe
-a----        17/05/2025      2:16          98256 taskhostw.exe
-a----        07/12/2019     10:09         101376 taskkill.exe
-a----        07/12/2019     10:09         106496 tasklist.exe
-a----        04/10/2025      2:04        1356296 Taskmgr.exe
-a----        18/10/2025      2:06         828472 tcblaunch.exe
-a----        04/12/2023      3:47         326144 TieringEngineService.exe
-a----        07/12/2019     10:08          73728 TpmInit.exe
-a----        14/04/2025      1:40         273920 TpmTool.exe
-a----        21/02/2025     18:47         102400 tpmvscmgr.exe
-a----        21/02/2025     18:47         143872 tpmvscmgrsvr.exe
-a----        04/12/2023      3:47         429056 tracerpt.exe
-a----        04/12/2023      3:47          69120 TSTheme.exe
-a----        13/06/2025      2:03          90624 TSWbPrxy.exe
-a----        21/02/2025     18:47         283688 ttdinject.exe
-a----        21/02/2025     18:47          86896 tttracer.exe
-a----        07/12/2019     10:09          70144 tzsync.exe
-a----        07/12/2019     10:08          59904 tzutil.exe
-a----        17/05/2025      2:16         177664 UCPDMgr.exe
-a----        07/12/2019     10:08          56632 ucsvc.exe
-a----        07/12/2019     15:58          55808 UevAppMonitor.exe
-a----        06/12/2019     22:28         265216 unregmp2.exe
-a----        07/12/2019     10:08         121392 upfc.exe
-a----        21/02/2025     18:48          52224 UPPrinterInstaller.exe
-a----        17/05/2025      2:16         102400 UserAccountControlSettings.exe
-a----        21/02/2025     18:47          54272 userinit.exe
-a----        17/05/2025      2:16         242688 UsoClient.exe
-a----        17/05/2025      2:16        1421312 usocoreworker.exe
-a----        17/05/2025      2:16         145920 UtcDecoderHost.exe
-a----        21/02/2025     18:47         126464 Utilman.exe
-a----        17/05/2025      2:16         724480 vds.exe
-a----        07/12/2019     10:08         177976 verifier.exe
-a----        07/12/2019     10:08         203264 verifiergui.exe
-a----        21/02/2025     18:48         320000 vfpctrl.exe
-a----        18/10/2025      2:06        3225488 vmcompute.exe
-a----        18/10/2025      2:06        2402296 vmwp.exe
-a----        07/12/2019     10:09         145920 vssadmin.exe
-a----        17/05/2025      2:16        1495040 VSSVC.exe
-a----        27/10/2025     17:24        2413504 vulkaninfo-1-999-0-0-0.exe
-a----        27/10/2025     17:24        2413504 vulkaninfo.exe
-a----        07/12/2019     10:08         108032 w32tm.exe
-a----        04/10/2025      2:04         112640 WaaSMedicAgent.exe
-a----        04/12/2023      3:48         329728 wbadmin.exe
-a----        17/05/2025      2:17        1617408 wbengine.exe
-a----        21/02/2025     18:48         107008 wecutil.exe
-a----        17/05/2025      2:16         577952 WerFault.exe
-a----        17/05/2025      2:16         180408 WerFaultSecure.exe
-a----        17/05/2025      2:16         237488 wermgr.exe
-a----        17/05/2025      2:16         281600 wevtutil.exe
-a----        07/12/2019     10:09         146944 wextract.exe
-a----        04/10/2025      2:05         966656 WFS.exe
-a----        07/12/2019     10:09          73728 whoami.exe
-a----        04/12/2023      3:47          98816 wiaacmgr.exe
-a----        04/12/2023      3:45         133608 wifitask.exe
-a----        04/12/2023      3:46         523120 wimserv.exe
-a----        13/06/2025      2:03          79360 WinBioDataModelOOBE.exe
-a----        17/05/2025      2:16          73216 Windows.WARP.JITService.exe
-a----        13/06/2025      2:03          80896 WindowsActionDialog.exe
-a----        17/05/2025      2:16          71680 WindowsUpdateElevatedInstaller.exe
-a----        04/10/2025      2:05         442728 wininit.exe
-a----        18/10/2025      2:05        1582088 winload.exe
-a----        04/10/2025      2:05         945152 winlogon.exe
-a----        18/10/2025      2:05        1231416 winresume.exe
-a----        07/12/2019     10:08          52736 winrs.exe
-a----        04/12/2023      3:47        2811392 WinSAT.exe
-a----        07/12/2019     10:09          59392 winver.exe
-a----        04/10/2025      2:05         316120 wkspbroker.exe
-a----        13/06/2025      2:03         462848 wksprt.exe
-a----        07/12/2019     10:08         103424 wlanext.exe
-a----        04/12/2023      3:46          69264 wlrmdr.exe
-a----        18/10/2025      2:06        1601024 WMPDMC.exe
-a----        21/02/2025     18:48         105472 WorkFolders.exe
-a----        04/12/2025     18:13         906584 wpbbin.exe
-a----        04/10/2025      2:04        1188064 WpcMon.exe
-a----        04/10/2025      2:04         289280 WpcTok.exe
-a----        04/10/2025      2:05         321536 wpr.exe
-a----        04/12/2023      3:46          95232 WSCollect.exe
-a----        17/05/2025      2:16         181760 wscript.exe
-a----        17/05/2025      2:17         171520 wsl.exe
-a----        18/11/2025     18:29          90112 wslconfig.exe
-a----        17/05/2025      2:16         120320 wsqmcons.exe
-a----        04/12/2023      3:46          94208 WSReset.exe
-a----        04/10/2025      2:04          94024 wuauclt.exe
-a----        04/10/2025      2:05         161776 WUDFCompanionHost.exe
-a----        04/10/2025      2:05         304128 WUDFHost.exe
-a----        17/05/2025      2:16         345088 wusa.exe
-a----        17/05/2025      2:16         996256 WWAHost.exe
-a----        07/12/2019     10:09          50688 xcopy.exe
-a----        07/12/2019     10:09          64000 xwizard.exe

```

6. Muestra los ficheros de este directorio que tengan extensión `.dll`, ordenados por fecha de creación y mostrando únicamente las propiedades de fecha de creación (`CreationTime`), último acceso (`LastAccessTime`) y nombre (`Name`).
```bash
PS C:\WINDOWS\system32> Get-ChildItem | Where-Object { $_.Extension -eq ".dll" } `
| Sort-Object CreationTime `
| Select-Object CreationTime, LastAccessTime, Name
18/10/2025 2:05:38  10/12/2025 18:25:28 CloudExperienceHostCommon.dll
18/10/2025 2:05:38  09/12/2025 23:49:15 cdd.dll
18/10/2025 2:05:38  10/12/2025 18:14:50 cryptngc.dll
18/10/2025 2:05:38  10/12/2025 18:17:55 NgcCtnrSvc.dll
18/10/2025 2:05:38  10/12/2025 18:25:39 ngcsvc.dll
18/10/2025 2:05:38  08/12/2025 19:17:50 ngcpopkeysrv.dll
18/10/2025 2:05:46  08/12/2025 20:08:03 EdgeContent.dll
18/10/2025 2:05:46  10/12/2025 18:14:50 WindowsCodecs.dll
18/10/2025 2:05:46  24/11/2025 2:02:47  msscntrs.dll
18/10/2025 2:05:46  10/12/2025 18:15:32 mssitlb.dll
18/10/2025 2:05:46  10/12/2025 18:24:51 mssph.dll
18/10/2025 2:05:46  09/11/2025 20:58:11 Search.ProtocolHandler.MAPI2.dll
18/10/2025 2:05:46  10/12/2025 18:26:23 mssvp.dll
18/10/2025 2:05:46  10/12/2025 18:14:49 mssprxy.dll
18/10/2025 2:05:46  10/12/2025 18:25:26 mssrch.dll
18/10/2025 2:05:47  10/12/2025 18:14:49 tquery.dll
18/10/2025 2:05:47  10/12/2025 18:25:28 InputService.dll
18/10/2025 2:05:47  08/12/2025 20:07:53 EditBufferTestHook.dll
18/10/2025 2:05:47  10/12/2025 18:25:43 WordBreakers.dll
18/10/2025 2:05:47  10/12/2025 18:25:27 Windows.UI.Core.TextInput.dll
18/10/2025 2:05:47  10/12/2025 18:14:49 TextInputFramework.dll
18/10/2025 2:05:47  10/12/2025 18:25:28 InputLocaleManager.dll
18/10/2025 2:05:47  09/12/2025 23:49:09 ISM.dll
18/10/2025 2:05:47  10/12/2025 18:25:26 TileDataRepository.dll
18/10/2025 2:05:47  10/12/2025 18:32:46 LicenseManager.dll
18/10/2025 2:05:47  10/12/2025 18:14:49 windows.storage.dll
18/10/2025 2:05:47  10/12/2025 18:17:49 AppXDeploymentClient.dll
18/10/2025 2:05:48  10/12/2025 18:15:19 wintrust.dll
18/10/2025 2:05:48  10/12/2025 18:17:51 Windows.StateRepository.dll
18/10/2025 2:05:48  10/12/2025 18:14:49 Windows.StateRepositoryPS.dll
18/10/2025 2:05:48  10/12/2025 18:25:26 Windows.StateRepositoryBroker.dll
18/10/2025 2:05:48  10/12/2025 18:25:26 Windows.StateRepositoryClient.dll
18/10/2025 2:05:48  10/12/2025 18:18:14 Windows.StateRepositoryCore.dll
18/10/2025 2:05:48  09/11/2025 20:58:11 Windows.StateRepositoryUpgrade.dll
18/10/2025 2:05:48  10/12/2025 18:25:26 StateRepository.Core.dll
18/10/2025 2:05:48  10/12/2025 18:25:26 wpncore.dll
18/10/2025 2:05:48  10/12/2025 18:14:50 user32.dll
18/10/2025 2:05:48  10/12/2025 18:14:50 win32u.dll
18/10/2025 2:05:49  18/11/2025 19:00:47 MusUpdateHandlers.dll
18/10/2025 2:05:49  10/12/2025 18:25:29 SettingsEnvironment.Desktop.dll
18/10/2025 2:05:50  10/12/2025 18:17:53 aeinv.dll
18/10/2025 2:05:50  10/12/2025 18:17:53 invagent.dll
18/10/2025 2:05:50  09/11/2025 20:57:32 win32appinventorycsp.dll
18/10/2025 2:05:51  09/12/2025 23:49:09 uDWM.dll
18/10/2025 2:05:51  09/12/2025 23:49:09 dwmcore.dll
18/10/2025 2:05:51  10/12/2025 18:14:50 wuceffects.dll
18/10/2025 2:05:51  10/12/2025 18:17:49 ci.dll
18/10/2025 2:05:51  10/12/2025 18:14:48 combase.dll
18/10/2025 2:05:51  10/12/2025 18:14:49 wincorlib.dll
18/10/2025 2:05:51  10/12/2025 18:14:49 WinTypes.dll
18/10/2025 2:05:51  10/12/2025 18:17:49 ncryptprov.dll
18/10/2025 2:05:51  10/12/2025 18:26:03 lsasrv.dll
18/10/2025 2:05:51  09/11/2025 20:57:46 offlinelsa.dll
18/10/2025 2:05:51  09/12/2025 21:25:41 hal.dll
18/10/2025 2:05:51  10/12/2025 18:18:31 ntdll.dll
18/10/2025 2:05:52  10/12/2025 18:23:21 shlwapi.dll
18/10/2025 2:05:52  10/12/2025 18:18:16 shell32.dll
18/10/2025 2:05:53  08/12/2025 0:51:57  SCardSvr.dll
18/10/2025 2:05:53  09/11/2025 20:57:58 SCardDlg.dll
18/10/2025 2:05:53  08/12/2025 0:51:57  certprop.dll
18/10/2025 2:05:53  08/12/2025 20:07:52 ScDeviceEnum.dll
18/10/2025 2:05:53  08/12/2025 20:08:03 SCardBi.dll
18/10/2025 2:05:53  10/12/2025 18:14:50 sppobjs.dll
18/10/2025 2:05:53  10/12/2025 18:14:50 sppwinob.dll
18/10/2025 2:05:53  28/11/2025 18:34:15 LicensingDiagSpp.dll
18/10/2025 2:05:53  08/12/2025 20:08:11 sppcomapi.dll
18/10/2025 2:05:53  04/12/2025 18:13:21 EditionUpgradeHelper.dll
18/10/2025 2:05:53  09/11/2025 20:57:57 EditionUpgradeManagerObj.dll
18/10/2025 2:05:53  09/11/2025 20:57:57 DeviceReactivation.dll
18/10/2025 2:05:53  08/12/2025 20:07:54 LicensingWinRT.dll
18/10/2025 2:05:53  10/12/2025 18:17:48 enterprisecsps.dll
18/10/2025 2:05:53  10/12/2025 18:17:48 dmenrollengine.dll
18/10/2025 2:05:53  10/12/2025 18:25:26 Windows.Internal.Management.dll
18/10/2025 2:05:53  09/11/2025 20:57:40 DMAlertListener.ProxyStub.dll
18/10/2025 2:05:54  10/12/2025 18:25:26 dui70.dll
18/10/2025 2:05:54  04/12/2025 18:13:55 GdiPlus.dll
18/10/2025 2:05:54  10/12/2025 18:14:49 urlmon.dll
18/10/2025 2:05:54  10/12/2025 18:14:49 iertutil.dll
18/10/2025 2:05:54  10/12/2025 18:25:28 msIso.dll
18/10/2025 2:05:54  10/12/2025 18:25:28 edgeIso.dll
18/10/2025 2:05:54  18/11/2025 19:00:59 BootMenuUX.dll
18/10/2025 2:05:54  08/12/2025 20:07:50 ReAgent.dll
18/10/2025 2:05:54  10/12/2025 18:17:50 ReInfo.dll
18/10/2025 2:05:54  10/12/2025 18:17:55 AppXDeploymentServer.dll
18/10/2025 2:05:54  10/12/2025 18:18:16 AppXDeploymentExtensions.onecore.dll
18/10/2025 2:05:54  10/12/2025 18:18:16 AppXDeploymentExtensions.desktop.dll
18/10/2025 2:05:54  10/12/2025 18:26:43 nlasvc.dll
18/10/2025 2:05:54  10/12/2025 18:17:51 nlaapi.dll
18/10/2025 2:05:54  10/12/2025 18:14:49 ncsi.dll
18/10/2025 2:05:54  09/11/2025 20:57:53 Print.Workflow.Source.dll
18/10/2025 2:05:54  08/12/2025 23:35:16 PrintWorkflowService.dll
18/10/2025 2:05:55  08/12/2025 20:07:55 Windows.Graphics.Printing.Workflow.dll
18/10/2025 2:05:55  09/11/2025 20:57:53 Windows.Graphics.Printing.Workflow.Native.dll
18/10/2025 2:05:55  10/12/2025 18:17:53 Print.PrintSupport.Source.dll
18/10/2025 2:05:55  01/12/2025 20:24:42 rasmontr.dll
18/10/2025 2:05:55  08/12/2025 0:51:57  mprdim.dll
18/10/2025 2:05:55  09/11/2025 20:57:54 rtm.dll
18/10/2025 2:05:55  08/12/2025 20:08:05 iprtprio.dll
18/10/2025 2:05:55  08/12/2025 20:08:05 iprtrmgr.dll
18/10/2025 2:05:55  08/12/2025 20:07:51 mprapi.dll
18/10/2025 2:05:55  10/12/2025 18:25:48 rasman.dll
18/10/2025 2:05:55  08/12/2025 0:51:57  rasmans.dll
18/10/2025 2:05:55  04/12/2025 18:14:03 rastapi.dll
18/10/2025 2:05:55  10/12/2025 18:26:03 lsm.dll
18/10/2025 2:05:55  10/12/2025 18:14:49 winsta.dll
18/10/2025 2:05:55  10/12/2025 18:25:27 twinui.dll
18/10/2025 2:05:55  10/12/2025 18:25:27 windowsudk.shellcommon.dll
18/10/2025 2:05:57  08/12/2025 20:08:11 iumcrypt.dll
18/10/2025 2:05:57  04/12/2025 18:14:08 ngctasks.dll
18/10/2025 2:06:01  08/12/2025 19:13:06 bcastdvruserservice.dll
18/10/2025 2:06:01  09/11/2025 20:57:56 NgcIsoCtnr.dll
18/10/2025 2:06:01  10/12/2025 18:17:49 ssdpapi.dll
18/10/2025 2:06:01  08/12/2025 0:51:57  ssdpsrv.dll
18/10/2025 2:06:01  09/11/2025 20:57:31 hvloader.dll
18/10/2025 2:06:01  30/11/2025 2:37:27  kdhvcom.dll
18/10/2025 2:06:01  18/11/2025 18:50:27 iumbase.dll
18/10/2025 2:06:01  09/11/2025 20:57:31 iumdll.dll
18/10/2025 2:06:01  04/12/2025 18:13:49 vertdll.dll
18/10/2025 2:06:01  09/11/2025 20:57:31 ucrtbase_enclave.dll
18/10/2025 2:06:01  09/11/2025 20:57:34 tcbloader.dll
18/10/2025 2:06:01  30/11/2025 2:37:29  skci.dll
18/10/2025 2:06:01  04/12/2025 18:14:04 CodeIntegrityAggregator.dll
18/10/2025 2:06:02  10/12/2025 18:25:45 mispace.dll
18/10/2025 2:06:02  10/12/2025 18:25:45 smphost.dll

``` 
7. Muestra el tamaño (`Length`) y nombre completo (`FullName`) de todos los ficheros del directorio ordenados por tamaño en sentido descendente.

```bash
PS C:\WINDOWS\system32> Get-ChildItem | Sort-Object Length -Descending | Select-Object Length, FullName
         C:\Windows\system32\WinBioDatabase
          C:\Windows\system32\WinBioPlugIns
          C:\Windows\system32\zh-CN
          C:\Windows\system32\zh-TW
          C:\Windows\system32\WinMetadata
          C:\Windows\system32\winrm
          C:\Windows\system32\WDI
          C:\Windows\system32\ti-et
          C:\Windows\system32\tr-TR
          C:\Windows\system32\Tasks
          C:\Windows\system32\th-TH
          C:\Windows\system32\wbem
          C:\Windows\system32\WCN
          C:\Windows\system32\uk-UA
          C:\Windows\system32\UNP
          C:\Windows\system32\ShellExperiences
          C:\Windows\system32\my-mm
          C:\Windows\system32\nb-NO
          C:\Windows\system32\MsDtc
          C:\Windows\system32\MUI
          C:\Windows\system32\nl-NL
          C:\Windows\system32\Nui
          C:\Windows\system32\NDF
          C:\Windows\system32\networklist
          C:\Windows\system32\MSDRM
          C:\Windows\system32\lxss
          C:\Windows\system32\MailContactsCalendarSync
          C:\Windows\system32\lt-LT
          C:\Windows\system32\lv-LV
          C:\Windows\system32\migwiz
          C:\Windows\system32\MRT
          C:\Windows\system32\Microsoft
          C:\Windows\system32\migration
          C:\Windows\system32\oobe
          C:\Windows\system32\Recovery
          C:\Windows\system32\restore
          C:\Windows\system32\ras
          C:\Windows\system32\RasToast
          C:\Windows\system32\SecureBootUpdates
          C:\Windows\system32\setup
          C:\Windows\system32\ro-RO
          C:\Windows\system32\ru-RU
          C:\Windows\system32\pt-PT
          C:\Windows\system32\PerceptionSimulation
          C:\Windows\system32\pl-PL
          C:\Windows\system32\OpenSSH
          C:\Windows\system32\osa-Osge-001
          C:\Windows\system32\ProximityToast
          C:\Windows\system32\pt-BR
          C:\Windows\system32\PointOfService
          C:\Windows\system32\Printing_Admin_Scripts
```
8. Muestra el tamaño y nombre completo de todos los ficheros del directorio que tengan un tamaño superior a 10MB (10000000 bytes) ordenados por tamaño.
```bash
PS C:\WINDOWS\system32> Get-ChildItem | Where-Object {$_.Length -gt 10000000} | Sort-Object Length | Select-Object Length, FullName

   Length FullName
   ------ --------
 10563584 C:\WINDOWS\system32\wmp.dll
 10577560 C:\WINDOWS\system32\onnxruntime.dll
 12989880 C:\WINDOWS\system32\ntoskrnl.exe
 14022088 C:\WINDOWS\system32\vmms.exe
 17874944 C:\WINDOWS\system32\Windows.UI.Xaml.dll
 19492864 C:\WINDOWS\system32\HologramWorld.dll
 20438440 C:\WINDOWS\system32\amdhip64_6.dll
 21762472 C:\WINDOWS\system32\amdhip64.dll
 24121344 C:\WINDOWS\system32\mshtml.dll
 25260032 C:\WINDOWS\system32\Hydrogen.dll
 26071040 C:\WINDOWS\system32\edgehtml.dll
 27976608 C:\WINDOWS\system32\mfxplugin64_hw.dll
 36242888 C:\WINDOWS\system32\vmfirmwarehcl.dll
 60357040 C:\WINDOWS\system32\OneDriveSetup.exe
105433000 C:\WINDOWS\system32\amd_comgr.dll
110283176 C:\WINDOWS\system32\amd_comgr_2.dll
113353968 C:\WINDOWS\system32\amdxc64.so
215625816 C:\WINDOWS\system32\MRT.exe


```
9. Muestra el tamaño y nombre completo de todos los ficheros del directorio que tengan un tamaño superior a 10MB y extensión `.exe` ordenados por tamaño.
```bash
PS C:\Windows\system32> Get-ChildItem | Where-Object { $_.Extension -eq ".exe" -and $_.Length -gt 10000000 } `
>> | Sort-Object Length | Select-Object Length, FullName                                                                              
   Length FullName
   ------ --------
 10859424 C:\Windows\system32\ntoskrnl.exe
215625816 C:\Windows\system32\MRT.exe

```

---
[Volver al índice](../../index.md)