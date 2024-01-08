# proxmox hardware
Description of Hardware setup for Home lab environment  

## PVE01
Physical Proxmox Virtual Environment Server 1  
Powered-on: Always  
WOL: enabled  

#### Hardware
Dell 3060M (dell micro)  
Intel Core i5-9500T (6cores)  
32GB SO-DIMM DDR4 RAM
1GBit Network interface  
M2 Samsung PM9A1 512GB M2 NVME  
M2 Google Coral TPU A/E key (wifi/bluetooth m2 slot)  
USB Conbee2 Zigbee dongle (extension cable 2mtr)  

#### VM & LXC
Current Virtual machines and lxc containers.  

#### Configs

##### Grub bootloader
To be able to passthrough the Google Coral TPU M2 (pci-e) to Virtual machines in Proxmox, some edits needs to be done in the Grub boot loader. Edit those lines in the PVE shell interface.  
![image](https://github.com/kippesikgithub/proxmox_hardware/assets/100353268/51a79f4b-a887-45e1-9d19-c059c60b139a)  
command: nano /etc/default/grub  
grub_config  

##### Interfaces
![image](https://github.com/kippesikgithub/proxmox_hardware/assets/100353268/9d4b6f01-cba3-4acf-a712-731efbfce806)  
command: nano /etc/network/interfaces  
interfaces_config  

##### Crontab
Since the Proxmox Backup server is turned off almost always, and only powered-on when making backups, we want to prevent error messages about backups volumes not reachable. To enable and disable backup volumes on the PVE machines, add lines to crontab in PVE shell interface.  
![image](https://github.com/kippesikgithub/proxmox_hardware/assets/100353268/e68bac36-3d30-4187-a3bd-2880aa48437b)  
command: crontab-e  
crontab_config  

## PVE02
Physical Proxmox Virtual Environment Server 2  
Powered-on: Only when somebody home
Powered-off: When nobody home for 4hr+ or Home assistant Holiday mode is activated  
WOL: enabled (wake up server from Home assistant interface)  

#### Hardware
Dell 3050M (dell micro)  
Intel Core i5-8500T (4cores)  
24GB SO-DIMM DDR4 RAM
1GBit Network interface  
M2 Kioxa 256GB M2 NVME  
M2 Google Coral TPU A/E key (wifi/bluetooth m2 slot)  
SATA HDD Seagate 5TB 2,5inch  
USB Conbee2 Zigbee dongle (extension cable 2mtr)  

#### VM & LXC
Current Virtual machines and lxc containers.  

#### Configs

## PVE03
Physical Proxmox Backup server
Powered-on: Nightly 1:00 - 3:00  
Powered-off: Nightly when backups are finished  
WOL: enabled (wake up server from Home assistant interface)  

#### Hardware
