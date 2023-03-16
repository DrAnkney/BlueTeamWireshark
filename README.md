# BlueTeamWireshark
Using Wireshark to capture and explore packets from red team scanning and exploits

*Required resources: Wireshark, Nmap*

*Optional resources: Metasploit, Apache*

## Docker Set-up

Download the Docker YML file and save it to your VM (we used Ubuntu for this). Navigate to the folder where you saved the file, and run
```
sudo docker-compose pull
```

After the first use, for any subsequent experiments, run 
```
sudo docker-compose up -d.
```

Once you’re done with the container,
```
sudo docker-compose down
```
will decompose the network.

## Wireshark Set-up

With the container running, open a terminal to look for the 192.168.13.1/24 system
```
ip a
```
![1 ip a command to find where to capture packets](https://user-images.githubusercontent.com/20114904/225680599-ec905c03-e255-476e-bb00-ace54846b26a.gif)

Note that if you have needed to decompose the docker container and recompose it later, the network ID (highlighted) will change (as you will see in the sample Wireshark screenshots below); repeat this step as needed.

In Wireshark, find that network ID, highlight it, and press Capture (on the top, in gray, but clickable):
![2 find that id in wireshark](https://user-images.githubusercontent.com/20114904/225682392-d0548696-032c-4c2e-99e7-fdb2a24905df.gif)

A pop-up will ask you to confirm that you want to start packet capture; push start at the bottom right:
![3 confirm choice of network](https://user-images.githubusercontent.com/20114904/225682615-746fc24d-7ab4-4516-943a-6358925ef25e.gif)

## Nmap Scan

Go back to the terminal and run 
```
nmap 192.168.13.1/24
```

A few things to notice: nmap starts with an ARP broadcast to ask who is at each address in the CIDR range we’ve given it. For those addresses that respond, Nmap then initiates a TCP 3-way handshake (transmission control protocol) with each on 1,000 ports (default). In the image below, the 21/tcp, 22/tcp etc etc mean that the port responded via the TCP handshake protocol and is running the service listed:
![4 nmap](https://user-images.githubusercontent.com/20114904/225683397-15a2e2e5-4ff5-40c5-8d1b-246d4a5043cf.gif)

Back in Wireshark, you can watch all of these packets flow through, from the ARP broadcasts to the 3-way handshakes (SYN, SYN-ACK, ACK):
![Nmap packet capture with ARP and TCP](https://user-images.githubusercontent.com/20114904/225685660-c776a239-35a8-4f76-ad0c-8b93c77a82b1.png)

Using different Nmap tags while watching Wireshark capture packets is an interesting exercise in understanding the different protocols used by different tags, the different speeds of scans, and which ports are scanned (for example, with the -F fast scan tag), among other scan properties. It's one thing to memorize, learn, and even use these tags, and it is quite another to watch the packets fly. I recommend playing with those before moving on to...

## Metasploit Exploits

The network in this Docker container is vulnerable to several Metasploit exploits (two require Apache to be installed; the rest can be done without Apache). Once you have had the fun of exploring those, I recommend going back over those exploits with Wireshark running. Two recommendations as you do this:

### Capture in Small Shark Bites
If you want to study what these exploits will look like in a packet capture, having one file per exploit will allow you to narrow down your field of view and began to generate an understanding. You want to be able to find these exploits in large packet captures, but you need to see what they look like before you can recognize them, so keeping it small is a good learning technique.

### Keep Good Notes with Screenshots
You are likely used to taking notes when hacking a system, but adding screenshots of which packets showed you what you needed to know will be a great addition to those notes. 

Happy Wiresharking!!
