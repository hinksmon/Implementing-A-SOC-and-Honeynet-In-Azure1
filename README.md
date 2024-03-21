# Implementing-A-SOC-and-Honeynet-In-Azure1
 In this Lab I setup Azure Sentinel (SIEM) and connect it to a live virtual machine acting as a honey pot. The primary focus will be to observe live attacks (RDP Brute Force) from all around the world. I used a custom PowerShell script to look up the attackers Geolocation information and plot it on the Azure Sentinel Map


# Skills Learned
- Setting up a Honeypot 
- Setting up a SIEM on Azure Sentinel
- Cloud based SIEM creation
- Monitoring and logging attacks from our honeypot
- Proficiency in analyzing and interpreting network logs.
- Configuring Firewalls 

   

Tools Used
[Bullet Points - Remove this afterwards]

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Microsoft Azure
- Microsoft Sentinel
- Virtual Machiene

Steps
1. In the first step I created a VM inn Azure that would be exposed to the internet to draw people in to collect traffic.



2. Secondly I configured the VM firewall traffic to allow ALL types of inbound traffic so that I could make it as visibile as possible to threat actors.



3. Thirdly I created a log analytics workspace so I could injest the windows event logs from the VM to get our own custom log that has geolocation in it that will injest ito our SIEM.



4. Then I logged on to the VM and went to event viewer and used a IPGeolocation website to get a script for the custom log we are making to get location coordinates for our map.



5.  After that I used the custom script to and tried to fail to log in to my VM again to generate log traffic to see if it would develop coordinates.



6.  After the log is successfully up and running I went to Azure to implement the log to our log analytics workspace so I could connect the script to my SIEM.



7.  Next I needed to set up seperate the raw data collected into categories for the different geolocation artifacts collected from the event logs in the VM (latitude/longitude/country/etc).



8. Lastly to setup the world map with the pinged artifacts that I parsed before I used a scripted with all the firels i used to seperate the data and plugged them into my map (FAILED_RDP_WITH_GEO_CL | summarize event_count=count() by sourcehost_CF, latitude_CF, longitude_CF, country_CF, label_CF, destinationhost_CF
| where destinationhost_CF != "samplehost"
| where sourcehost_CF != ").



9. Then I let it sit for a while to collect more traffic and this was the end result.




