#	Filter 
```
Using this script we are running tshark parallely and analysis the output at regular interval of time.
```
##	deauth process
This function is called at regular interval of time, this function will check each file in the directory and if that file is not pre processed  earlier then it will filter the required data from that file.


## data.conf
This file will contain the required inputs.
- __mac_addresses__  : List of mac address on which filter need to be applied.
-  __filters_collection__ : List of filter which you want to apply on each file.
## interface
The interface on which you want to run the Wireshark for capturing the packets.


## CAPTURE_FILE_PREFIX
file name in which you want to save.


## Sample data.conf file

```
[DEFAULT]  
mac_addresses = b0:44:9c:04:99:0d, b0:44:9c:04:98:c6, b0:44:9c:04:96:73, b0:44:9c:04:99:1c  
filters_collection = wlan.fc.type_subtype==12, wlan.fc.type_subtype==27, wlan.fc.type_subtype==36,tcp  
INTERFACE = \\Device\\NPF_{582A59C3-EBA4-4902-88BA-74D698AF38D6}  
CAPTURE_FILE_PREFIX = sniffer_local_host
```


## How to run
```
python3 filter.py
```
