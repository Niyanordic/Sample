# Serial Observer


This document explains how to execute the `serial_observer.py` script for Wi-Fi scanning and pattern detection.

## Below are the explanation of parameters

	 

 

-	__port__  :white_check_mark: *Required Parameters*  ```  The Port on Which you want to run.```
 -	__patterns__ :white_check_mark:  *Required Parameters*   It is a list containing dict as parameters.
	-	_name_: log_file_name: The name of the file where the matched pattern output will be stored.
	-	_level_ : The log level to match.
	-	_pattern_: The regular expression pattern to be matched in the input stream

- __file_name__ :x: - ~~Required Paramters~~ It contains a list of commands that need to be sent through the specified port. This data will be transmitted over the port for execution or processing.
	Sample of file_name.conf is below :blush:	:page_facing_up:
	```
	wifi scan
	wifi connect -s TPLINK_ARCHER_C9_24G -k 1 -p 12345678
	net ping 192.168.1.178
	net stats
	wifi status
	wifi statistics
	wifi disconnect
	kernel uptime -p
	```
				
		








---
##  :pushpin: Execution Format
```
python file.py --port "port_name" --patterns "list[dict]" --file_name "file.conf"
```

##  :rocket: Execution Example

```bash
python serial_observer.py --port "/dev/ttyACM9" --patterns '[{"name": "connection_request_failed", "level": "info", "pattern": "(?i)\\bConnection request failed\\s+\\(Wrong password/2\\)"}]' --file_name "test_collection.conf"

```
