## Network Forensic Analysis Report
### Time Thieves

You must inspect your traffic capture to answer the following questions:

1.What is the domain name of the users' custom site?

Frank-n-ted.com

2.What is the IP address of the Domain Controller (DC) of the AD network?

Domain Controller is 10.6.12.12

3.What is the name of the malware downloaded to the 10.6.12.203 machine?
Once you have found the file, export it to your Kali machine's desktop.

http://205.185.125.104/files/june11.dll

4.Upload the file to VirusTotal.com

<img width="1440" alt="Screen Shot 2021-05-15 at 12 37 39 PM" src="https://user-images.githubusercontent.com/65127312/119914041-668ecc00-bf2d-11eb-989c-004026655a76.png">

5.What kind of malware is this classified as?

Trojan.

## Vulnerable Windows Machine

1.Find the following information about the infected Windows machine:
 - Hostname: Rotterdam-PC
 - IP address: 172.16.4.205
 - MAC address: LenovoEM_b0:63:a4

2.What is the username of the Windows user whose computer is infected?

Matthijs.devries

3.What are the IP addresses used in the actual infection traffic?

185.243.115.84

## Illegal Downloads

IT was informed that some users are torrenting on the network. The Security team does not forbid the use of torrents for legitimate purposes, such as downloading operating systems. However, they have a strict policy against copyright infringement.

IT shared the following about the torrent activity:

 - The machines using torrents live in the range 10.0.0.0/24 and are clients of an AD domain.
 - The DC of this domain lives at 10.0.0.2 and is named DogOfTheYear-DC.
 - The DC is associated with the domain dogoftheyear.net.

Your task is to isolate torrent traffic and answer the following questions:

1.Find the following information about the machine with IP address 10.0.0.201:

  - MAC address: 00:16:17:18:66:c8

  - Windows username: elmer.blanco

  - Computer host name: BLANCO-DESKTOP
