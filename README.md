# Maltree

<p align="center">
<img src="https://user-images.githubusercontent.com/14183473/108923102-d7a4a780-75fd-11eb-8e28-f0049611d6d5.png"/>
</p><br>

Maltree is a SOC (security operations center) solution that uses a working agent that statically and dynamically analyzes potential suspect files. From there Maltree's working sensor sends the files to a cloud ELK server where a security analyst analyzes the results and determines the steps to take from there. For more information or to talk about how we can use Maltree to secure your environment please contact us at **contact@penetrum.com**.

# Malcore

Malcore is the main core engine of Maltree's analysis. Malcore performs static and dynamic analysis on passed files by doing the following;

_NOTE: * == binary only_

 - Binary file identification*
 - Produces x86 ASM instructions*
 - Produces likely shellcode*
 - Automatic architecture detection*
 - Hexdump of the file
 - Readable strings found inside of the raw file 
 - Detection of imports, exports, and sections*
 - Obtains the following hashes:
   - SHA-1
   - SHA-256
   - SHA-512
   - MD5
   - ImpHash*
   - SSDeep hash*
 - Runs the file through over 700 Yara rules*
 - Produces a custom Yara rule by grabbing the most interesting strings*
 - Full dynamic analysis*
 - And much more
 
A free version of Malcore without the extra ammenties will be released soon.

# Malnet

We are here today to talk about Malnet since most of the issues in this repository will be from the Malnet engine. Malnet is a the RESTful API of Maltree which processes all files passed to it through Malcore. Malnet uses a state of the art API key system to determine what output will be produced to the user and does full static and dynamic analysis on any uploaded file in under 5 minutes (<50MB). We achieve this by running a fully static analysis on the file first gathering hexdumps, strings, architecture type, and PE information (if present). From there we perform a fully dynamic analysis in a sandboxed environment and watch what the file does. From there Malnet produces all of the same output as Malcore but in a JSON format. For more information or to talk about how we can use Malnet to secure your environment please contact us at **contact@penetrum.com**
