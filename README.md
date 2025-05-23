# Kippesik Repository
Welcome to my github repository, where you can find everything regarding our Proxmox environment, Home Assistant environment and beyond. You can find details and config (examples), information and explanation in this repo's.  
Choosing the hardware for your setup: https://github.com/kippesikgithub/proxmox_hardware/blob/main/choosing_hardware.md  
Choosing the right Operating system: https://github.com/kippesikgithub/proxmox_hardware/blob/main/choosing_operating_system.md  
How To Install Proxmox: https://github.com/kippesikgithub/proxmox_hardware/blob/main/install_proxmox.md  
Want to know more about our Home Assistant Setup: https://github.com/kippesikgithub/proxmox_haos  
Want to know more about our Home Assistant Interface: https://github.com/kippesikgithub/ha_cards_interface  
Want to know more about our Birdnet install: https://github.com/kippesikgithub/birdnet_install  
TTeck Proxmox Helper Scripts: https://tteck.github.io/Proxmox/  

# Proxmox HomeLab Setup
![image](https://github.com/kippesikgithub/proxmox_hardware/assets/100353268/81dd9d3f-46b1-4e24-82df-2ac8e78132d9)

# PVE01
![image](https://github.com/kippesikgithub/proxmox_hardware/assets/100353268/3ac955a4-0c3e-4253-a3b8-72d3de5ea0c0)  
Physical Proxmox Virtual Environment Server 1  
Powered-on: Always  
WOL: enabled  

### Hardware
Dell 3050M (dell micro)  
Intel Core i5-9500T (6cores)  
32GB SO-DIMM DDR4 RAM  
1GBit Network interface  
M2 Samsung PM9A1 512GB M2 NVME  
M2 Google Coral TPU A/E key (wifi/bluetooth m2 slot)  
USB Conbee2 Zigbee dongle (extension cable 2mtr)  

#### Configs
###### Grub bootloader
To be able to passthrough the Google Coral TPU M2 (pci-e) to Virtual machines in Proxmox, some edits needs to be done in the Grub boot loader. Edit those lines in the PVE shell interface.  
![image](https://github.com/kippesikgithub/proxmox_hardware/assets/100353268/51a79f4b-a887-45e1-9d19-c059c60b139a)  
command: nano /etc/default/grub  
grub_config  

###### Interfaces
![image](https://github.com/kippesikgithub/proxmox_hardware/assets/100353268/9d4b6f01-cba3-4acf-a712-731efbfce806)  
command: nano /etc/network/interfaces  
interfaces_config  

###### Crontab
Since the Proxmox Backup server is turned off almost always, and only powered-on when making backups, we want to prevent error messages about backups volumes not reachable. To enable and disable backup volumes on the PVE machines, add lines to crontab in PVE shell interface.  
![image](https://github.com/kippesikgithub/proxmox_hardware/assets/100353268/e68bac36-3d30-4187-a3bd-2880aa48437b)  
command: crontab-e  
crontab_config  

### VM & LXC
![image](https://github.com/kippesikgithub/proxmox_hardware/assets/100353268/92a23f71-2ff8-4d17-b046-8be6782eae04)  
Current Virtual machines and lxc containers.  

#### Home Assistant
HAOS Proxmox VM  
6-cores  
32GB RAM  
Google Coral TPU M2 passthrough (frigate)  
100GB Diskspace on 512GB nvme m2 drive  
Home Assistant is the Smarthome platform I already use for over 7 years.

##### Links
Home Assistant Operating system: https://github.com/kippesikgithub/proxmox_haos  
Home Assistant Interface: https://github.com/kippesikgithub/ha_cards_interface  
Frigate Setup: https://github.com/kippesikgithub/frigate  

#### InfluxDB
Proxmox LXC  
2-cores  
4GB RAM  
50GB Diskspace on 512GB nvme m2 drive  
InfluxDB stores all the data, real-time, coming from Home Assistant in the Influx Database. In InfluxDB I keep the whole history of data, to be able to Visualise this via Grafana.

##### Links
InfluxDB setup: https://github.com/kippesikgithub/influxdb_in_proxmox  


# PVE02
![image](https://github.com/kippesikgithub/proxmox_hardware/assets/100353268/a2c23de5-c9cf-4071-bd5d-27aa684873a8)  
Physical Proxmox Virtual Environment Server 2  
Powered-on: Only when somebody home
Powered-off: When nobody home for 4hr+ or Home assistant Holiday mode is activated  
WOL: enabled (wake up server from Home assistant interface)  

### Hardware
Dell 3070M (dell micro)  
Intel Core i5-6400T (4cores)  
24GB SO-DIMM DDR4 RAM  
1GBit Network interface  
M2 WDC SN180 1TB NVME  
SATA HDD Seagate 5TB 2,5inch  
USB3 HDD Seagate 4TB 2,5inch  

#### Configs

### VM & LXC
![image](https://github.com/kippesikgithub/proxmox_hardware/assets/100353268/9e568dfd-f1c7-469d-a912-635e9e5f3de7)  
Current Virtual machines and lxc containers.  

#### Openmediavault NAS Storage
Proxmox Virtual Machine  
#### JellyFin
Proxmox LXC  
Mounts NFS volume 'Media' from the NAS Storage.  
#### Sabnzbd
Proxmox LXC  
Mounts NFS volume 'Downloads' from the NAS Storage.  
#### Grafana
Proxmox LXC  
Connects to InfluxDB server on PVE01.  
#### Spotweb
Proxmox LXC  
#### BirdNetPi
Detects singing birds using RTSP audio feeds.  

# PVE03
Physical Proxmox Backup server
Powered-on: Nightly 1:00 - 3:00  
Powered-off: Nightly when backups are finished  
WOL: enabled (wake up server from Home assistant interface)  

#### Hardware

## Handy Links
### Add bigger HDD to Dell Micro pc (2.5inch 4TB or 5TB)
Link: https://www.dell.com/community/en/conversations/optiplex-desktops/15mm-25-drive-in-3060-micro/647f8401f4ccf8a8de2db9ad  
Modify Caddy, only keep side parts, put HDD screws in it.  
![image](https://github.com/kippesikgithub/proxmox_hardware/assets/100353268/13808224-3d06-4a06-8ddf-2e235ab7ad58)
