#	filter.py
```
This script runs `tshark` in parallel and analyzes the output at regular time intervals.
```

The required input parameters are specified in the `data.conf` file.

## Sample : -> data.conf file

```
[DEFAULT]  
dut_mac_addresses = b0:44:9c:04:99:0d, b0:44:9c:04:98:c6, b0:44:9c:04:96:73, b0:44:9c:04:99:1c  
filters_collection = wlan.fc.type_subtype==12, wlan.fc.type_subtype==27, wlan.fc.type_subtype==36,tcp  
interface =  \Device\NPF_{9482A529-D16E-4CDA-812C-B02F1211F788}  
capture_file_prefix = sniffer_local_host  
interval = 50
```

## data.conf
An overview of each input parameter is provided below.
- __dut_mac_addresses__  : A comma-separated list of MAC addresses on which the filter should be applied.
-  __filters_collection__ : A comma-separated list of filters to be applied to each `.pcap` file.
 - __interface__ The network interface on which Wireshark will run to capture packets.
- __capture_file_prefix__  The prefix to be used for naming the capture files.
- __interval__ Specifies the duration (in seconds) for which Wireshark will run before saving each capture to a new file.



## How to run
```
python3 filter.py
```


## Output 

The output will be stored in a file.  
For each `.pcap` file, two tables will be generated: one for control frames and another for data frames.
Additionally, there will be two global tables—one for control frames and one for data frames—that will consolidate the corresponding tables from all `.pcap` files.
