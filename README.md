# Snort configuration


In my third project i wanted to configure and build my own IDS/IPS and i looked for open source options and after some research i choose snort.
Snort its one of the most used IDS/IPS frameworks in the industry.



![alt text](https://github.com/fabianvagi91/IDS-using-snort-and-packet-analyisis/blob/03560447230900fdd7fc42d12d25e5b910c86597/depedencies..jpg)

The First step before installing snort we have to install the dependencies required for snort to run.
First i installed the  libdaq-dev package that is a development library related to the Data Acquisition (DAQ) framework, commonly used for data collection and processing in various applications, including scientific research, engineering, and automation.
Using sudo install -y i can install multiple packages.

![alt text](https://github.com/fabianvagi91/IDS-using-snort-and-packet-analyisis/blob/912772a7c7ce312a238b61470bf658905cb80a0b/hwlocdependency2.jpg)

The hwloc package (short for Hardware Locality) is a library designed for the management and abstraction of hardware resources in a computing environment.

![alt text](https://github.com/fabianvagi91/IDS-using-snort-and-packet-analyisis/blob/912772a7c7ce312a238b61470bf658905cb80a0b/LauJIT%20dependency.jpg)
![alt text](https://github.com/fabianvagi91/IDS-using-snort-and-packet-analyisis/blob/912772a7c7ce312a238b61470bf658905cb80a0b/LauJIT%20install%20dependency.jpg)
LauJIT is a Just-In-Time (JIT) compiler designed primarily for the Lua programming language. It aims to improve the performance of Lua scripts by translating Lua bytecode into machine code at runtime.

![alt text](https://github.com/fabianvagi91/IDS-using-snort-and-packet-analyisis/blob/912772a7c7ce312a238b61470bf658905cb80a0b/libdaq%20dependency.jpg)
![alt text](https://github.com/fabianvagi91/IDS-using-snort-and-packet-analyisis/blob/912772a7c7ce312a238b61470bf658905cb80a0b/libdaq%20dependency%20recompilation.jpg)

The libdaq.git repository typically refers to the Git repository for the libdaq library, which is part of the Data Acquisition (DAQ) framework. This repository contains the source code and related files for the library.


![alt text](https://github.com/fabianvagi91/IDS-using-snort-and-packet-analyisis/blob/a6fa22d1527dc7727ab508bef581e1efa6875ea2/snort%20communitary%20rules.jpg)

Snort community rules are an essential resource for anyone using Snort as their intrusion detection system. They provide a collaborative and cost-effective way to enhance network security by detecting a wide range of threats.

A rule is a specific instruction that defines how to identify and respond to network traffic.

![alt text](https://github.com/fabianvagi91/IDS-using-snort-and-packet-analyisis/blob/912772a7c7ce312a238b61470bf658905cb80a0b/snort%20library%20install.jpg)

./configure_cmake.sh is a shell script typically included in the source distribution of the software. It sets up the build environment for CMake. Running this script prepares the configuration files needed for the build process.

--prefix /usr/local/snort  This option specifies the installation directory for the software. By using --prefix, you’re telling the build system to install Snort into the /usr/local/snort directory instead of the default location (which is usually /usr/local or /usr).


![alt text](https://github.com/fabianvagi91/IDS-using-snort-and-packet-analyisis/blob/912772a7c7ce312a238b61470bf658905cb80a0b/snort%20config.jpg)
This is the configuration file and we can edit using sudo nano /etc/snort/snort.lua
HOME_NET  is a variable that defines the range of IP addresses considered part of your internal or trusted network in this case is the NAT network that i created in my virtual machine
ips  its the intrusion prevension system and is where we can upload our rule set. In my case i set the communitary rules 
Outputs its the variable when we can define where we store and read alerts and logs, this is crucial for monitoring and responding to security events effectively.

![alt text](https://github.com/fabianvagi91/IDS-using-snort-and-packet-analyisis/blob/912772a7c7ce312a238b61470bf658905cb80a0b/snort%20running%20script.jpg)

Now that the configuration is set im going to run snort in my network.

-snort This is the command to run the Snort application
- -c this option specifies the path to the configuration file that Snort should use.
- /usr/local/snort/etc/snort/snort.lua  This is the path to the configuration file you want Snort to use.
- -i eth0 specifies that Snort should listen on the network interface eth0 which is my network interface.

We can see that the communitary rules are correctly configurated and running

![alt text](https://github.com/fabianvagi91/IDS-using-snort-and-packet-analyisis/blob/912772a7c7ce312a238b61470bf658905cb80a0b/packet%20analyzing.jpg)

In order to analyze logs we need to generate traffic so i pinged 20 times to 8.8.8.8 and curl to recive GET request.
Also i created a .pcap file and dump the traffic so i can analyze with wireshark.

# Paquet analysis 

![alt text](https://github.com/fabianvagi91/IDS-using-snort-and-packet-analyisis/blob/912772a7c7ce312a238b61470bf658905cb80a0b/wireshark%20dns.jpg)
![alt text](https://github.com/fabianvagi91/IDS-using-snort-and-packet-analyisis/blob/912772a7c7ce312a238b61470bf658905cb80a0b/arp%20tcp%20and%20http.jpg)

We can see the traffic that comes from our network and analyze with wireshark.
I filtered Dns,tcp and http so i can see clearly the traffic destination.

# Conclusion

Must pay attention in the configuration file.
The current version of snort has the old configuration of 
