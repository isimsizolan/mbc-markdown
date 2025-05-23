<table>
<tr>
<td><b>ID</b></td>
<td><b>C0031</b></td>
</tr>
<tr>
<td><b>Objective(s)</b></td>
<td><b><a href="../cryptography">Cryptography</a></b></td>
</tr>
<tr>
<td><b>Related ATT&CK Techniques</b></td>
<td><b>None</b></td>
</tr>
<tr>
<td><b>Version</b></td>
<td><b>2.1</b></td>
</tr>
<tr>
<td><b>Created</b></td>
<td><b>13 October 2020</b></td>
</tr>
<tr>
<td><b>Last Modified</b></td>
<td><b>5 December 2023</b></td>
</tr>
</table>


# Decrypt Data

Malware may decrypt data. 

## Methods

|Name|ID|Description|
|---|---|---|
|**AES**|C0031.001|Malware decrypts data encrypted with the AES algorithm.|
|**Block Cipher**|C0031.002|Malware decrypts data encrypted with a block cipher.|
|**Blowfish**|C0031.003|Malware decrypts data encrypted with the Blowfish algorithm.|
|**Camellia**|C0031.004|Malware decrypts data encrypted with the Camellia algorithm.|
|**3DES**|C0031.005|Malware decrypts data encrypted with the 3DES algorithm.|
|**HC-128**|C0031.006|Malware decrypts data encrypted with the HC-128 algorithm.|
|**HC-256**|C0031.007|Malware decrypts data encrypted with the HC-256 algorithm.|
|**RC4**|C0031.008|Malware decrypts data encrypted with the RC4 algorithm.|
|**RC6**|C0031.009|Malware decrypts data encrypted with the RC6 algorithm.|
|**RSA**|C0031.010|Malware decrypts data encrypted with the RSA algorithm.|
|**Skipjack**|C0031.011|Malware decrypts data encrypted with the Skipjack block cipher algorithm.|
|**Sosemanuk**|C0031.012|Malware decrypts data encrypted with the Sosemanuk stream cipher.|
|**Stream Cipher**|C0031.013|Malware decrypts data encrypted with a stream cipher.|
|**Twofish**|C0031.014|Malware decrypts data encrypted with the Twofish algorithm.|

## Use in Malware

|Name|Date|Method|Description|
|---|---|---|---|
|[**BlackEnergy**](../../xample-malware/blackenergy.md)|2007|--|BlackEnergy encrypts or decrypts via WinCrypt. [[1]](#1)|
|[**Kovter**](../../xample-malware/kovter.md)|2016|--|Encrypt or decrypt via WinCrypt [[1]](#1)|
|[**Snake**](../../xample-malware/snake.md)|2004|C0031.001|Decrypts credential stores using AES [[2]](#2)|
|[**Snake**](../../xample-malware/snake.md)|2004|C0031.005|Decrypts .NET assembly with 3DES [[2]](#2)|

## Detection

|Tool: capa|Mapping|APIs|
|---|---|---|
|[encrypt or decrypt via WinCrypt](https://github.com/mandiant/capa-rules/blob/master/data-manipulation/encryption/encrypt-or-decrypt-via-wincrypt.yml)|Decrypt Data (C0031)|CryptEncrypt, CryptDecrypt, CryptAcquireContext, CryptGenKey, CryptImportKey|
|[decrypt data using AES via x86 extensions](https://github.com/mandiant/capa-rules/blob/master/data-manipulation/encryption/aes/decrypt-data-using-aes-via-x86-extensions.yml)|Decrypt Data::AES (C0031.001)|--|

|Tool: CAPE|Class|Mapping|APIs|
|---|--|---|---|
|[decryption](https://github.com/kevoreilly/CAPEv2/blob/master/modules/signatures/CAPE.py)|CAPE_Decryption|Decrypt Data (C0031)|CryptDecrypt|

## Code Snippets

### C0031 Snippet
<details>
<summary> Decrypt Data </summary>
SHA256: c86cbf5e78c9f05ecfc11e4f2c147781cef77842a457e19ba690477eb564c22b
<pre>
asm
push    ebx
mov     ebx, [esp+4+arg_4]
push    esi
lea     eax, [ebx+20h]
push    eax             ; unsigned int
call    ??2@YAPAXI@Z    ; operator new(uint)
mov     ecx, [esp+0Ch+arg_C]
mov     edx, eax
add     esp, 4
mov     esi, [ecx]
mov     [edx], esi
mov     esi, [ecx+4]
mov     [edx+4], esi
mov     ecx, [ecx+8]
mov     [edx+8], ecx
mov     edx, [esp+8+arg_8]
test    ebx, ebx
mov     [eax+0Ch], edx
jle     short loc_B
mov     esi, [esp+8+arg_0]
push    edi
mov     edi, 0FFFFFFFDh
lea     edx, [eax+3]
sub     edi, eax

loc_A:
mov     cl, [edx-3]
xor     cl, [edx+2]
xor     cl, [edx-1]
xor     cl, [edx]
mov     [edx+0Dh], cl
xor     [esi], cl
inc     edx
inc     esi
lea     ecx, [edi+edx]
cmp     ecx, ebx
jl      short loc_A
pop     edi

loc_B:
push    eax             ; void *
call    ??3@YAXPAX@Z    ; operator delete(void *)
add     esp, 4
mov     eax, 1
pop     esi
pop     ebx
retn

</pre>

## References

<a name="1">[1]</a> capa v4.0, analyzed at MITRE on 10/12/2022

<a name="2">[2]</a> https://www.cybereason.com/blog/research/threat-analysis-report-snake-infostealer-malware

