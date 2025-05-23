<table>
<tr>
<td><b>ID</b></td>
<td><b>E1082</b></td>
</tr>
<tr>
<td><b>Objective(s)</b></td>
<td><b><a href="../discovery">Discovery</a></b></td>
</tr>
<tr>
<td><b>Related ATT&CK Techniques</b></td>
<td><b>System Information Discovery (<a href="https://attack.mitre.org/techniques/T1082">T1082</a>)</b></td>
</tr>
<tr>
<td><b>Version</b></td>
<td><b>2.3</b></td>
</tr>
<tr>
<td><b>Created</b></td>
<td><b>2 August 2022</b></td>
</tr>
<tr>
<td><b>Last Modified</b></td>
<td><b>30 April 2024</b></td>
</tr>
</table>


# System Information Discovery

Malware may attempt to get detailed information about the system. This can include details about the operating system, hardware configurations, installed software, system uptime, and other system-level details.

See ATT&CK: **System Information Discovery ([T1082](https://attack.mitre.org/techniques/T1082/))**.

## Methods

|Name|ID|Description|
|---|---|---|
|**Generate Windows Exception**|E1082.m01|Malware may trigger an exception as a way of gathering system details.|
|**Enumerate Environment Variables**|E1082.m02|Malware may query environmental variables as a way of gathering system details.|

## Use in Malware

|Name|Date|Method|Description|
|---|---|---|---|
|[**TrickBot**](../xample-malware/trickbot.md)|2016|--|The malware can collect information about the computer, resources, services, installed programs, firmware, and operating system versions. [[7]](#7)|
|[**WebCobra**](../xample-malware/webcobra.md)|2018|--|Malware learns about the system so it can drop compatible miner software. [[8]](#8)|
|[**Ursnif**](../xample-malware/ursnif.md)|2016|--|Malware uses Window's command prompt commands to gather system info, task list, installed drivers, and installed programs.  [[1]](#1)|
|[**BlackEnergy**](../xample-malware/blackenergy.md)|2007|--|Malware uses Systeminfo to gather OS version, system configuration, BIOS, the motherboard, and processor. [[2]](#2)|
|[**DarkComet**](../xample-malware/dark-comet.md)|2008|--|Malware can collect information about the computer, resources, and operating system version.  [[3]](#3)|
|[**Emotet**](../xample-malware/emotet.md)|2018|--|Emotet collects information related to OS, processes, and sometimes mail client information and sends it to C2. [[4]](#4)|
|[**Stuxnet**](../xample-malware/stuxnet.md)|2010|--|Malware gathers information (OS version, workgroup status, computer name, domain/workgroup name, file name of infected project file) about each computer in the network to spread itself. [[5]](#5)|
|[**Stuxnet**](../xample-malware/stuxnet.md)|2010|--|Stuxnet checks OS version. [[5]](#5)|
|[**CHOPSTICK**](../xample-malware/chopstick.md)|2015|--|CHOPSTICK collects information from the host including Windows version, CPU architecture, and UAC settings. [[6]](#6)|
|[**CryptoLocker**](../xample-malware/cryptolocker.md)|2013|--|The malware queries environment variables. [[9]](#9)|
|[**Gamut**](../xample-malware/gamut.md)|2014|--|The malware queries environment variables. [[9]](#9)|
|[**GoBotKR**](../xample-malware/gobotkr.md)|2019|--|GoBotKR uses wmic, systeminfo and ver commands to collect information about the system and the installed software and queries environment variables. [[9]](#9) [[10]](#10)|
|[**Hupigon**](../xample-malware/hupigon.md)|2013|--|Hupigon queries environment variables. [[9]](#9)|
|[**Kovter**](../xample-malware/kovter.md)|2016|--|Kovter gets disk information. [[9]](#9)|
|[**Mebromi**](../xample-malware/mebromi.md)|2011|--|Mebromi checks OS version. [[9]](#9)|
|[**Redhip**](../xample-malware/redhip.md)|2011|--|Redhip checks the OS version. [[9]](#9)|
|[**Rombertik**](../xample-malware/rombertik.md)|2015|--|Rombertik gets the disk size. [[9]](#9)|
|[**Shamoon**](../xample-malware/shamoon.md)|2012|--|Shamoon gets the hostname. [[9]](#9)|
|[**UP007**](../xample-malware/up007.md)|2016|--|The malware queries environment variables. [[9]](#9)|
|[**Snake**](../xample-malware/snake.md)|2004|--|Snake gets the OS version, disk size, machine name, and geographic location [[11]](#11)|

## Detection

|Tool: capa|Mapping|APIs|
|---|---|---|
|[query environment variable](https://github.com/mandiant/capa-rules/blob/master/host-interaction/environment-variable/query-environment-variable.yml)|System Information Discovery (E1082)|kernel32.GetEnvironmentVariable, kernel32.GetEnvironmentStrings, kernel32.ExpandEnvironmentStrings, msvcr90.getenv, msvcrt.getenv, System.Environment::GetEnvironmentVariable, System.Environment::GetEnvironmentVariables, System.Environment::ExpandEnvironmentVariables|
|[get disk information](https://github.com/mandiant/capa-rules/blob/master/host-interaction/hardware/storage/get-disk-information.yml)|System Information Discovery (E1082)|kernel32.GetDriveType, kernel32.GetLogicalDrives, kernel32.GetVolumeInformation, kernel32.GetVolumeNameForVolumeMountPoint, kernel32.GetVolumePathNamesForVolumeName, kernel32.GetLogicalDriveStrings, kernel32.QueryDosDevice|
|[get disk size](https://github.com/mandiant/capa-rules/blob/master/host-interaction/hardware/storage/get-disk-size.yml)|System Information Discovery (E1082)|kernel32.GetDiskFreeSpace, kernel32.GetDiskFreeSpaceEx|
|[check OS version](https://github.com/mandiant/capa-rules/blob/master/host-interaction/os/version/check-os-version.yml)|System Information Discovery (E1082)|--|
|[get hostname](https://github.com/mandiant/capa-rules/blob/master/host-interaction/os/hostname/get-hostname.yml)|System Information Discovery (E1082)|kernel32.GetComputerName, kernel32.GetComputerNameEx, GetComputerObjectName, ws2_32.gethostname, gethostname|

|Tool: CAPE|Mapping|APIs|
|---|---|---|
|[antivm_generic_disk](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/antivm_generic_disk.py)|System Information Discovery (E1082)|DeviceIoControl, NtClose, NtCreateFile, NtDuplicateObject, NtOpenFile, NtDeviceIoControlFile|
|[recon_systeminfo](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/recon_systeminfo.py)|System Information Discovery (E1082)|--|
|[recon_beacon](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/recon_beacon.py)|System Information Discovery (E1082)|HttpOpenRequestA, HttpSendRequestA|
|[uses_adfind](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/uses_adfind.py)|System Information Discovery (E1082)|--|
|[antivm_generic_cpu](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/antivm_generic_cpu.py)|System Information Discovery (E1082)|--|
|[accesses_mailslot](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/accesses_netlogon.py)|System Information Discovery (E1082)|--|
|[accesses_netlogon_regkey](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/accesses_netlogon.py)|System Information Discovery (E1082)|--|
|[antivm_generic_bios](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/antivm_generic_bios.py)|System Information Discovery (E1082)|--|
|[antivm_hyperv_keys](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/antivm_hyperv_keys.py)|System Information Discovery (E1082)|--|
|[uses_windows_utilities_nltest](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/windows_utilities.py)|System Information Discovery (E1082)|--|
|[antivm_generic_scsi](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/antivm_generic_scsi.py)|System Information Discovery (E1082)|RegOpenKeyExW, RegQueryValueExA, RegQueryValueExW, RegOpenKeyExA|
|[antivm_parallels_keys](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/antivm_parallels_keys.py)|System Information Discovery (E1082)|--|
|[antivm_generic_diskreg](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/antivm_generic_diskreg.py)|System Information Discovery (E1082)|--|
|[antivm_generic_system](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/antivm_generic_system.py)|System Information Discovery (E1082)|--|
|[system_account_discovery_cmd](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/collects_systeminfo_cmd.py)|System Information Discovery (E1082)|--|
|[system_currently_loggedin_user_cmd](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/collects_systeminfo_cmd.py)|System Information Discovery (E1082)|--|
|[system_info_discovery_cmd](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/collects_systeminfo_cmd.py)|System Information Discovery (E1082)|--|
|[system_info_discovery_pwsh](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/collects_systeminfo_cmd.py)|System Information Discovery (E1082)|--|
|[system_network_discovery_cmd](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/collects_systeminfo_cmd.py)|System Information Discovery (E1082)|--|
|[system_network_discovery_pwsh](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/collects_systeminfo_cmd.py)|System Information Discovery (E1082)|--|
|[system_user_discovery_cmd](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/collects_systeminfo_cmd.py)|System Information Discovery (E1082)|--|
|[antivm_generic_services](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/antivm_generic_services.py)|System Information Discovery (E1082)|RegOpenKeyExW, RegEnumKeyExW, RegEnumKeyExA, RegOpenKeyExA|
|[antivm_generic_disk_setupapi](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/antivm_generic_disk_setupapi.py)|System Information Discovery (E1082)|SetupDiGetClassDevsA, SetupDiGetClassDevsW|
|[antisandbox_check_userdomain](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/antisandbox_check_userdomain.py)|System Information Discovery (E1082)|rtcEnvironBstr|
|[browser_scanbox](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/browser_scanbox.py)|System Information Discovery (E1082)|JsEval, COleScript_ParseScriptText, COleScript_Compile|
|[recon_fingerprint](https://github.com/CAPESandbox/community/tree/master/modules/signatures/windows/recon_fingerprint.py)|System Information Discovery (E1082)|--|

### E1082.m02 Snippet
<details>
<summary> System Information Discovery </summary>
SHA256: e4b36a1d4e70d988efa2ec27e5a639be5eb0880474f746851c13e56f007a8377
Location: 0x004017e9
<pre>
push    eax     ; push register to store return value onto the stack
push    u_ALLUSERSPROFILE_0041a9a4      ; push argument to function (name of the sought environment variable - in this case, ALLUSERSPROFILE)
call    dword ptr [->KERNEL32.DLL::GetEnvironmentVariableW]     ; call function to get environment variable value
</pre>
</details>

## References

<a name="1">[1]</a> https://www.trendmicro.com/vinfo/us/threat-encyclopedia/malware/PE_URSNIF.A2?_ga=2.131425807.1462021705.1559742358-1202584019.1549394279

<a name="2">[2]</a> https://blog-assets.f-secure.com/wp-content/uploads/2019/10/15163408/BlackEnergy_Quedagh.pdf

<a name="3">[3]</a> https://blog.malwarebytes.com/threat-analysis/2012/06/you-dirty-rat-part-1-darkcomet/

<a name="4">[4]</a> https://documents.trendmicro.com/assets/white_papers/ExploringEmotetsActivities_Final.pdf

<a name="5">[5]</a> https://docs.broadcom.com/doc/security-response-w32-stuxnet-dossier-11-en

<a name="6">[6]</a> https://web.archive.org/web/20210307034415/https://www.fireeye.com/content/dam/fireeye-www/global/en/current-threats/pdfs/rpt-apt28.pdf

<a name="7">[7]</a> https://www.securityartwork.es/wp-content/uploads/2017/07/Trickbot-report-S2-Grupo.pdf

<a name="8">[8]</a> https://www.mcafee.com/blogs/other-blogs/mcafee-labs/webcobra-malware-uses-victims-computers-to-mine-cryptocurrency/

<a name="9">[9]</a> capa v4.0, analyzed at MITRE on 10/12/2022

<a name="10">[10]</a> https://www.welivesecurity.com/2019/07/08/south-korean-users-backdoor-torrents/

<a name="11">[11]</a> https://www.cybereason.com/blog/research/threat-analysis-report-snake-infostealer-malware
