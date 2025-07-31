#	filter.py
```
Using this script we are running tshark parallely and analysis the output at regular interval of time.
```

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




#	mcs_parsing.py
This script is used for capturing   Data Rate   with retransmissions & without retransmissions for HE, HT, VHT, DSSS and Legacy.
## Sample Data.conf file

```
[HE]  
filter = radiotap.he.data_3.data_mcs <= 7 && wlan.fc.retry  
mcs = radiotap.he.data_3.data_mcs  
retry = wlan.fc.retry  
  
[HT]  
filter = radiotap.mcs.index && wlan.fc.retry  
mcs = radiotap.mcs.index  
retry = wlan.fc.retry  
  
[VHT]  
filter = wlan_radio.11ac.mcs && wlan.fc.retry  
mcs = wlan_radio.11ac.mcs  
retry = wlan.fc.retry  
  
[DSSS]  
filter = wlan_radio.data_rate  
mcs = wlan_radio.data_rate  
retry = wlan.fc.retry  
  
[Legacy]  
filter = wlan_radio.data_rate  
mcs = wlan_radio.data_rate  
retry = wlan.fc.retry
```

## How to run
```
python3 mcs_parsing.py
```
