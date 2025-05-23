<table>
<tr>
<td><b>ID</b></td>
<td><b>C0046</b></td>
</tr>
<tr>
<td><b>Objective(s)</b></td>
<td><b><a href="../file-system">File System</a></b></td>
</tr>
<tr>
<td><b>Related ATT&CK Techniques</b></td>
<td><b>None</b></td>
</tr>
<tr>
<td><b>Version</b></td>
<td><b>2.3</b></td>
</tr>
<tr>
<td><b>Created</b></td>
<td><b>4 December 2020</b></td>
</tr>
<tr>
<td><b>Last Modified</b></td>
<td><b>30 April 2024</b></td>
</tr>
</table>


# Create Directory

Malware creates a directory.

## Use in Malware

|Name|Date|Method|Description|
|---|---|---|---|
|[**Gamut**](../../xample-malware/gamut.md)|2014|--|Gamut creates directories. [[1]](#1)|
|[**GoBotKR**](../../xample-malware/gobotkr.md)|2019|--|GoBotKR creates directories. [[1]](#1)|
|[**GravityRAT**](../../xample-malware/gravity-rat.md)|2018|--|GravityRAT creates directories. [[1]](#1)|
|[**Hupigon**](../../xample-malware/hupigon.md)|2013|--|Hupigon creates directories. [[1]](#1)|
|[**Kovter**](../../xample-malware/kovter.md)|2016|--|Kovter creates directories. [[1]](#1)|
|[**Redhip**](../../xample-malware/redhip.md)|2011|--|Redhip creates directories. [[1]](#1)|
|[**UP007**](../../xample-malware/up007.md)|2016|--|UP007 creates directories. [[1]](#1)|

## Detection

|Tool: capa|Mapping|APIs|
|---|---|---|
|[create directory](https://github.com/mandiant/capa-rules/blob/master/host-interaction/file-system/create/create-directory.yml)|Create Directory (C0046)|kernel32.CreateDirectory, kernel32.CreateDirectoryEx, kernel32.CreateDirectoryTransacted, NtCreateDirectoryObject, ZwCreateDirectoryObject, SHCreateDirectory, SHCreateDirectoryEx, _mkdir, _wmkdir, System.IO.Directory::CreateDirectory, System.IO.DirectoryInfo::Create, System.IO.DirectoryInfo::CreateSubdirectory|

|Tool: CAPE|Class|Mapping|APIs|
|---|---|---|---|
|[arkei_files](https://github.com/CAPESandbox/community/blob/master/modules/signatures/windows/infostealer_arkei.py)|ArkeiFiles|Create Directory (C0046)|--|

### C0046 Snippet
<details>
<summary> File System::Create Directory </summary>
SHA256: 27253651170386863b148afb2a0fdda7780ae65cbc31405acbd99fa06b44b79f
Location: 0x1400036d4
<pre>
xor     param_2, param_2        ; use default security attributes (param_2 is NULL)
mov     param_1, rbp    ; use contents of rbp as directory name
call    qword ptr [->KERNEL32.DLL::CreateDirectoryA]  ; call Windows API to create directory
</pre>
</details>

## References

<a name="1">[1]</a> capa v4.0, analyzed at MITRE on 10/12/2022

