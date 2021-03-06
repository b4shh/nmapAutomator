# nmapAutomator

A script you can run in the background!
  
![nmapAutomator](https://i.imgur.com/3cMJIPr.gif)
  
## Summary

The main goal for this script is to automate the process of enumeration & recon that is run every time, and instead focus our attention on real pentesting.  
  
This will ensure two things:  
1. Automate nmap scans. 
2. Always have some recon running in the background. 

Once initial ports are found '*in 5-10 seconds*', we can start manually looking into those ports, and let the rest run in the background with no interaction from our side whatsoever.  

## Features

### Scans
1. **Quick:** Shows all open ports quickly (~15 seconds)  
2. **Basic:** Runs Quick Scan, then runs a more thorough scan on found ports (~5 minutes)  
3. **UDP:** Runs "Basic" on UDP ports (~5 minutes)  
4. **Full:** Runs a full range port scan, then runs a thorough scan on new ports (~5-10 minutes)  
5. **Vulns:** Runs CVE scan and nmap Vulns scan on all found ports (~5-15 minutes)  
6. **Recon:** Runs "Basic" scan "if not yet run", then suggests recon commands "i.e. gobuster, nikto, smbmap" based on the found ports, then prompts to automatically run them  
7. **All:** Runs all the scans consecutively (~20-30 minutes)  

*This is a reconnaissance tool, and it does not perform any exploitation.*

### Automatic Recon
With the `recon` option, nmapAutomator will automatically recommend and run the best recon tools for each found port.  
If a recommended tool is missing from your machine, nmapAutomator will suggest how to install it.

### Output
nmapAutomator saves the output of each type of scan is saved into a separate file, under the output directory.  
The entire script output is also saved, which you can view with `less -r outputDir/nmapAutomator_host_type.txt`, or you can simply `cat` it.

### POSIX Compatible
nmapAutomator is 100% POSIX compatible, so it can run on any `sh` shell, and on any `unix` machine.  
You can use it on any device that supports shells (*even a 10 YO router!*), which makes nmapAutomator ideal for lateral movement recon.

-----
  
## Requirements:
[ffuf](https://github.com/ffuf/ffuf), which we can install with:
```bash
sudo apt update
sudo apt install ffuf -y
```

Or [Gobuster](https://github.com/OJ/gobuster) '*v3.0 or higher*', which we can install with:  
```bash
sudo apt update
sudo apt install gobuster -y
```

Other recon tools used within the script include:
|[nmap Vulners](https://github.com/vulnersCom/nmap-vulners)|[sslscan](https://github.com/rbsec/sslscan)|[nikto](https://github.com/sullo/nikto)|[joomscan](https://github.com/rezasp/joomscan)|[wpscan](https://github.com/wpscanteam/wpscan)|
|:-:|:-:|:-:|:-:|:-:|
|[droopescan](https://github.com/droope/droopescan)|[smbmap](https://github.com/ShawnDEvans/smbmap)|[enum4linux](https://github.com/portcullislabs/enum4linux)|[dnsrecon](https://github.com/darkoperator/dnsrecon)|[odat](https://github.com/quentinhardy/odat)|
|[smtp-user-enum](https://github.com/pentestmonkey/smtp-user-enum)|snmp-check|snmpwalk|ldapsearch||

  
Most of these should be installed by default in [Parrot OS](https://www.parrotsec.org) and [Kali Linux](https://www.kali.org).  
*If any recon recommended tools are found to be missing, they will be automatically omitted, and the user will be notified.*
  
## Installation:
```bash
git clone https://github.com/21y4d/nmapAutomator.git
sudo ln -s $(pwd)/nmapAutomator/nmapAutomator.sh /usr/local/bin/
```

-----

## Usage:
```
./nmapAutomator.sh -h
Usage: ./nmapAutomator.sh -H/--host <TARGET-IP> -t/--type <TYPE> [-d/--dns <DNS SERVER> -o/--output <OUTPUT DIRECTORY>]

Scan Types:
	Quick: Shows all open ports quickly (~15 seconds)
	Basic: Runs Quick Scan, then runs a more thorough scan on found ports (~5 minutes)
	UDP  : Runs "Basic" on UDP ports "requires sudo" (~5 minutes)
	Full : Runs a full range port scan, then runs a thorough scan on new ports (~5-10 minutes)
	Vulns: Runs CVE scan and nmap Vulns scan on all found ports (~5-15 minutes)
	Recon: Suggests recon commands, then prompts to automatically run them
	All  : Runs all the scans (~20-30 minutes)
```

**Example scans**:
```
./nmapAutomator.sh --host 10.1.1.1 --type All
./nmapAutomator.sh -H 10.1.1.1 -t Basic
./nmapAutomator.sh -H academy.htb -t Recon -d 1.1.1.1
```

------

## Upcoming Features
- [x] Support URL/DNS - Thanks @KatsuragiCSL
- [x] Add extensions fuzzing for http recon
- [x] Add an nmap progress bar
- [x] List missing tools in recon
- [x] Add option to change output folder
- [x] Save full script output to a file
- [x] Improve performance and efficiency of the script - Thanks @caribpa
- [x] Make nmapAutomater 100% POSIX compatible. - Massive Thanks to @caribpa
- [ ] Add network scanning type, so nmapAutomator can discover live hosts on the network.
- [ ] Enable usage of multiple scan types in one scan.
- [ ] Enable scanning of multiple hosts in one scan.
- [ ] Add remote mode, which uses bash only without any external tools (for lateral movement in a network)


**Feel free to send your pull requests :)**  
*For any pull requests, please try to follow these [Contribution Guidelines](CONTRIBUTING.md).*
