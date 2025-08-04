#	Sniffer Capture

-   Captures and analyzes Wi-Fi packets using `tshark`.
-   Operates in two modes:
    -  **Pre Processing**: Captures live packets from the specified network interface and analyzes them simultaneously at regular intervals.
    -   **Post Processing**: Processes existing `.pcap` files from current directory.
  


			                        ┌─────────────────────┐
			                        │    Start Script     │
			                        └─────────┬───────────┘
			                                  │
			                  ┌───────────────▼────────────────┐
			                  │ Check `preProcessing` setting  │
			                  └───────┬────────────────┬────────┘
			                          │                │
			                  ┌───────▼──────┐  ┌──────▼────────┐
			                  │ preProcessing│  │ preProcessing │
			                  │     = yes    │  │     = no      │
			                  └───────┬──────┘  └──────┬────────┘
			                          │                │
			        ┌─────────────────▼───┐     ┌──────▼────────────────┐
			        │ Run `tshark` in      │     │ Read existing         │
			        │ parallel to capture  │     │ `.pcap` files         │
			        └─────────┬────────────┘     └──────────┬────────────┘
			                  │                              │
			        ┌─────────▼────────────┐       ┌─────────▼────────────┐
			        │ Apply filters during │       │ Apply filters to     │
			        │ live capture         │       │ captured files       │
			        └─────────┬────────────┘       └─────────┬────────────┘
			                  │                              │
			        ┌─────────▼────────────┐                 |
			        │ Store output tables  |                 |
			        for each file          │◄──────-─────────▼
			        └─────────┬────────────┘                 │
			                  │                              │
			        ┌─────────▼────────────┐                 │
			        │ Create consolidated  │◄────────────────┘
			        │ 	    tables     │    
			        └──────────────────────┘


The required input parameters are specified in the `data.conf` file.

## A sample `data.conf` file is shown below.
If preProcessing =1
```
[DEFAULT]  
dut_mac_addresses = b0:44:9c:04:99:0d, b0:44:9c:04:98:c6, b0:44:9c:04:96:73, b0:44:9c:04:99:1c  
interface =  \Device\NPF_{9482A529-D16E-4CDA-812C-B02F1211F788}  
capture_file_prefix = sniffer_local_host  
interval = 50
snaplen = 512
preProcessing=1
```
preProcessing = 0
```
[DEFAULT]  
dut_mac_addresses = b0:44:9c:04:99:0d, b0:44:9c:04:98:c6, b0:44:9c:04:96:73, b0:44:9c:04:99:1c  
interface = 
capture_file_prefix = 
interval =
snaplen = 
preProcessing =0
```
Note: ```interface, capture_file_prefix, interval, snaplen is not required in prePocessing is set to 0```
## Parameter Info.
An overview of each input parameter is provided below.
- __dut_mac_addresses__  : A comma-separated list of MAC addresses on which the filter should be applied.
 - __interface__ The network interface on which Wireshark will run to capture packets.
- __capture_file_prefix__  The prefix to be used for naming the capture files.
- __interval__ Specifies the duration (in seconds) for which Wireshark will run before saving each capture to a new file.
- __snaplen__ Specifies the snapshot length — the maximum number of bytes to capture from each packet.
- __preProcessing__   A flag that determines whether live packet capture and real-time analysis (pre-processing) should be performed.



## How to run
```
python3 filter.py
```


## Output 

The output will be stored in a file.  
For each `.pcap` file, two tables will be generated: one for control frames and another for data frames.
Additionally, there will be two global tables—one for control frames and one for data frames—that will consolidate the corresponding tables from all `.pcap` files.

![Sniffer Capture Output](https://github.com/Niyanordic/Sample/blob/main/sniffer_capture.png)


