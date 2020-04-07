# Maltree (under development)

Maltree is a tool that does full static analysis on malware samples. Maltree comes complete with the following features;

 - Automatic binary file identification (to determine what sandbox to run under)
 - Ability to take a single sample or a zip file of samples
 - Multiple outputs including HTML, JSON, and basic text output
 - Assembly instruction generation
 - Shellcode generation
 - Automatic architecture detection
 - Full hexdump of the binary itself
 - Detection of imports, exports, and sections within the binary
 - Fully customized detection of readable strings within the binary
 - Obtains the SHA1, SHA256, MD5, and ImpHash of the binary
 - Uploads the file to both Hybrid-Analysis and VirusTotal for detection checking and outputs the URL to the upload
 - Database support, and adds a searchable database
 - Automatic issue reporting

Maltree has the advantage of performing a full static analysis on malware samples without going through the manual effort. It does all of the above and saves the information for future use as well. The HTML is implemented so that it will fit inside of a body tag and be able to be customized right off the bat.
 
# Examples of Maltree

Searching Maltree's database. In order to perform a search on Maltree's database all you need to do is pass the `-s` flag. This will pull all stored SHA256 hashes from the database and provide you with them in a numbered list:

```
python .\maltree -s
[1] bebdb82d4edf3ccde78c3072f47abdecd31b43ecad525f95a2d5b3b8459d6921
[2] aa5f607076433086f6259131c4ba155b6f2587569f7fb0f21a0a4cdda225bd98
```

From there to grab all the information out of the database all you need to do is pass the `-sH` flag followed by your hash choice:

```
python maltree -sH aa5f607076433086f6259131c4ba155b6f2587569f7fb0f21a0a4cdda225bd98 | more
2
aa5f607076433086f6259131c4ba155b6f2587569f7fb0f21a0a4cdda225bd98
0x402000:       _CorExeMain

No exports
.text:  7.04781472482
.sdata: 6.61831635345
.rsrc:  0.705078264904
.reloc: 0.101910425663

32
0000000001:     4d5a90000300000004000000        MZ..........
0000000002:     ffff0000b800000000000000        ............
0000000003:     400000000000000000000000        @...........
0000000004:     000000000000000000000000        ............
0000000005:     000000000000000000000000        ............
0000000006:     800000000e1fba0e00b409cd        ............
0000000007:     21b8014ccd21546869732070        !..L.!This.p
0000000008:     726f6772616d2063616e6e6f        rogram.canno
0000000009:     742062652072756e20696e20        t.be.run.in.
0000000010:     444f53206d6f64652e0d0d0a        DOS.mode....
0000000011:     240000000000000050450000        $.......PE..
0000000012:     4c01040028355d5800000000        L...(5]X....
0000000013:     00000000e0000e010b010600        ............
0000000014:     003a0a00008c020000000000        .:..........
...
```

Maltree will also accept a single file and check if the data is inside of the database by searching the SHA256 hash. If the file is found it will output the data in a format of your choice, such as HTML:

```
python maltree -f UPS_PACK.tst --html | more
<div class='all-hashes'>
<p class='name'>SHA256 hash: bebdb82d4edf3ccde78c3072f47abdecd31b43ecad525f95a2d5b3b8459d6921</p>
</div>
<div class='basic-analysis'>
<div class='discovered-imports-class'>
<p class='basic-analysis-title-name'>Discovered Imports:</p>
<ul class='imports-list-names'>
<li>Location: 0x402000: Name: _CorExeMain</li>
</ul></div>
<div class='discovered-exports-class'>
<p class='basic-analysis-title-name'>Discovered Exports:</p>
<p class='nothing-found'>No exports</p>
<div class='discovered-sections-names'>
<p class='basic-analysis-title-name'>Discovered Sections:</p>
...
```

Or JSON:

```
python maltree -f UPS_PACK.tst --json | more
{
    "hashes": {
        "sha1": null,
        "sha256": "bebdb82d4edf3ccde78c3072f47abdecd31b43ecad525f95a2d5b3b8459d6921",
        "imphash": null,
        "md5": null
    },
    "basics": {
        "imports": "0x402000:\t_CorExeMain\n",
        "exports": "No exports",
        "sections": ".text:\t7.21362604625\n.rsrc:\t4.23402008341\n.reloc:\t0.101910425663\n",
        "architecture": 32
    },
    "scan_results": {
        "hybrid_analysis": "https://www.hybrid-analysis.com/search?query=bebdb82d4edf3ccde78c3072f47abdecd31b43ecad525f95a2d5b3b8459d6921",
        "virustotal": "https://www.virustotal.com/file/bebdb82d4edf3ccde78c3072f47abdecd31b43ecad525f95a2d5b3b8459d6921/analysis/1586195270/"
    },
...
```

Or basic text:

```
python maltree -f UPS_PACK.tst | more
Discovered Imports:
--------------------
Location: 0x402000:     Imported resource: _CorExeMain

Discovered Exports:
--------------------
No exports discovered

Identified Sections:
--------------------
Entropy: 7.21362604625  Name: .text:
Entropy: 4.23402008341  Name: .rsrc:
Entropy: 0.101910425663 Name: .reloc:

Runnable on: 32bit systems
--------------------
...
```

If the file hash is not found within the database it will do a full static analysis of the file itself. Examples of the assembly instructions that are generated from Maltree include the following;

```
Assembly instructions (first 50 instructions):
dec     ebp
pop     edx
nop
inc     eax
push    cs
pop     ds
push    cs
dec     esp
push    esp
outsd   dx, dword ptr [esi]
popal
insd    dword ptr es:[edi], dx
popal
outsb   dx, byte ptr [esi]
outsb   dx, byte ptr [esi]
outsd   dx, dword ptr [esi]
outsb   dx, byte ptr [esi]
outsb   dx, byte ptr [esi]
inc     esp
dec     edi
push    ebx
insd    dword ptr es:[edi], dx
outsd   dx, dword ptr [esi]
push    eax
inc     ebp
dec     esp
xchg    eax, ebx
pop     esi
inc     eax
inc     eax
inc     eax
dec     edi
inc     eax
pushal
dec     eax
pushal
inc     eax
push    es
push    es
inc     eax
inc     eax
insb    byte ptr es:[edi], dx
outsd   dx, dword ptr [esi]
pushal
inc     eax
inc     edx
dec     eax
inc     ebp
inc     edi
push    es
...
```

Strings:

```
Discovered strings (first 50 lines):
QwE]
4e3w{
_selectedService
lblUser
txtUsername
y(h5
}2`^
Z&,2w
fXR[
n@~9
w~De
<requestedPrivileges
$z{K
"qH!1
DangNhap.formCauHinh.resources
E'<':
pG]!
'<bA
nflzy
TargetFrameworkAttribute
TextBoxBase
_=;!#
\-R$
O23A
q~@@
OkRV
tV`4;
,%Kk
"L?^
b}&E
47\{
set_RightToLeftAutoMirrorImage
+qcv
h1KQt
K+UQ
5}<k-7
GE8$
ck],
</requestedPrivileges>
$N$A-
i,L/fV
rzgo
TFKh
lYJT
hb]KX
get_Controls
RFZJ,
`AIc
S8~=D
a(*E
...
```

And shellcode:

```
Shellcode (first 50 characters):\uMuZu\uxu9u0u\uxu0u0u\uxu0u3u\uxu0u0u\uxu0u0u\uxu0u0u\uxu0u4u\uxu0u0u\uxu0u0u\uxu0u0u\uxufufu\uxuf
```

Maltree also accepts a zip file of malware to be passed to it:

```
python maltree -z samples.zip | more
Discovered Imports:
--------------------
Location: 0x402000:     Imported resource: _CorExeMain

Discovered Exports:
--------------------
No exports discovered

Identified Sections:
--------------------
Entropy: 7.04781472482  Name: .text:
Entropy: 6.61831635345  Name: .sdata:
Entropy: 0.705078264904 Name: .rsrc:

...

Discovered Imports:
--------------------
Location: 0x402000:     Imported resource: _CorExeMain

Discovered Exports:
--------------------
No exports discovered

Identified Sections:
--------------------
Entropy: 7.21362604625  Name: .text:
Entropy: 4.23402008341  Name: .rsrc:
Entropy: 0.101910425663 Name: .reloc:

Runnable on: 32bit systems
--------------------
```

# Contact Us

To learn more about Maltree and the advantages and disadvantages of it, feel free to contact us at `contact@penetrum.com`. We will be happy to answer all your questions. There will be an opensourced version released to the general public once the development process is completed.
