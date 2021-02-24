# Malcore

<p align="center">
<img height="200" width="300" src="https://user-images.githubusercontent.com/14183473/108923102-d7a4a780-75fd-11eb-8e28-f0049611d6d5.png"/> ©
</p><br>


Malcore is the future of sandbox analysis. Malcore is the main engine of Maltree that does full static analysis on passed files and is able to with 99.99% reliability determine the difference between file types. Passed files produce the following information:

### Binary files

 - Dissassembly asm
 - Imports and exports 
 - Sections in the binary

### APK files

 - Manifest details
 - Permission details

### Doc files

 - Every doc file is ran through [Inquest DFI](https://labs.inquest.net/dfi) in a closed enviroment

### All files

 - Strings
 - Hexdump

### Interesting Features

 - Fuzzy hash matching at a 0.21% match ratio
 - Dissassembly of compiled binary files
 - Faster than the leading sandbox solutions
 - Integrated static analysis of Windows PE, ELF, APK, and all leading MS doc files (xls, xlsx, doc, docx, etc)
 - Mimetype guessing and exif data gathering
 - Full PCAP analysis for IP address and domains processed through [ZETAlytics](https://zetalytics.com/)
 - Generates yara rules and ndb signatures of each file passed
 - Runs each file through over 700+ well documented yara rules

# Malnet

Malnet is the RESTful API that processes all requests into Malcore, you can read the API documentation [here](http://173.79.10.115:9080/apidocs). During testing we were able to send up to 40,000 requests per hour to Malnet without the API failing. Malnet requires an API key which you may purchase from us on our [website](https://penetrum.com), or if you prefer you can contact us at the link below for a more private discussion. Key features of Malnet include:

 - Ability to search the database using a SHA-256 hash
 - Ability to check if a file is packed
 - Ability to perform deep static analysis on passed files
 - Ability to process uploads


### Interest Features

 - Unique UUID generated for each upload
 - Shellcode analysis 
 - Domain analysis processed by [ZETAlytics](https://zetalytics.com/)
 - Ability to process two PCAP files and discover the differences between them

# Malroot

COMING SOON ...

# Malbug 

COMING SOON ...

# Malbox

Malbox is the dynamic analysis environment for Malcore that integrates the static and dynamic analysis into the system. Malbox key features include:

 - Integratable with almost all Virtual Machine software (vbox, esxi, etc)
 - Runs multiple virtual machines including Windows 10, Ubuntu, and Android images
 - Traces calls produced by the sample passed to it
 - Full machine memory dump

# Maltree

Maltree is the whole thing put together into a package that is integratable into almost all major SOC solutions. The goal of Maltree is to provide a more stable, reliable, and cost effective malware analysis platform to integrate into your SOC solution.

# Road Map

COMING SOON ...


# **Penetrum LLC** <img src="https://penetrum.com/res/img/hand_logo_black.png" width=50 height=50 />

###### Contact information: <br> Email: contact@penetrum.com <br> Phone Number: +1 (703) 268-4350 <br> Copyright © 2021-2025 All Rights Reserved Penetrum LLC
