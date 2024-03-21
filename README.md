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

![image](https://github.com/hinksmon/Implementing-A-SOC-and-Honeynet-In-Azure1/assets/162920003/0238c341-12c6-4af6-86bd-3476ea9a0d80)


2. Secondly I configured the VM firewall traffic to allow ALL types of inbound traffic so that I could make it as visibile as possible to threat actors.

![image](https://github.com/hinksmon/Implementing-A-SOC-and-Honeynet-In-Azure1/assets/162920003/ef84e7a6-dda2-4930-8673-8b44ee68c544)


3. Thirdly I created a log analytics workspace so I could injest the windows event logs from the VM to get our own custom log that has geolocation in it that will injest ito our SIEM.

![image](https://github.com/hinksmon/Implementing-A-SOC-and-Honeynet-In-Azure1/assets/162920003/3c2a853d-6c1e-44d5-ad0d-1730122380d5)


4. Then I logged on to the VM and went to event viewer and used a IPGeolocation website to get a script for the custom log we are making to get location coordinates for our map.

![image](https://github.com/hinksmon/Implementing-A-SOC-and-Honeynet-In-Azure1/assets/162920003/392fbb0c-f889-49f7-9b7f-e29cc4b26de2)


5.  After that I used the custom script to and tried to fail to log in to my VM again to generate log traffic to see if it would develop coordinates.

![IMG_1347](https://github.com/hinksmon/Implementing-A-SOC-and-Honeynet-In-Azure1/assets/162920003/bc806de0-30f8-453d-a947-b55c5e608f5a)


6.  After the log is successfully up and running I went to Azure to implement the log to our log analytics workspace so I could connect the script to my SIEM.

![image](https://github.com/hinksmon/Implementing-A-SOC-and-Honeynet-In-Azure1/assets/162920003/20bb82f0-62a8-4728-8eab-840349f2c7a7)


7.  Next I needed to set up seperate the raw data collected into categories for the different geolocation artifacts collected from the event logs in the VM (latitude/longitude/country/etc).


![IMG_1356](https://github.com/hinksmon/Implementing-A-SOC-and-Honeynet-In-Azure1/assets/162920003/4ad0ac2e-31e5-4b98-a829-88e740566d92)


8. Lastly to setup the world map with the pinged artifacts that I parsed before I used a scripted with all the firels i used to seperate the data and plugged them into my map (FAILED_RDP_WITH_GEO_CL | summarize event_count=count() by sourcehost_CF, latitude_CF, longitude_CF, country_CF, label_CF, destinationhost_CF
| where destinationhost_CF != "samplehost"
| where sourcehost_CF != ").

![image](https://github.com/hinksmon/Implementing-A-SOC-and-Honeynet-In-Azure1/assets/162920003/25de029d-3fca-45c2-b1eb-f1e7662d4498)


9. Then I let it sit for a while to collect more traffic and this was the end result.


![image](https://github.com/hinksmon/Implementing-A-SOC-and-Honeynet-In-Azure1/assets/162920003/dc09caa3-254a-48e0-94fe-a170d95827c5)


