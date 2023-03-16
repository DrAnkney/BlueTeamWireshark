# BlueTeamWireshark
Using Wireshark to capture and explore packets from red team scanning and exploits

*Required resources: Wireshark, Nmap*

*Optional resources: Metasploit, Apache*

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

## Nmap Scans

