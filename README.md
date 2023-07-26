# Mikrotik-scripts
Here are some scripts for Mikrotik ROS 7.

## L2TP protection scripts
**firewall.src** - This is the fist stage of ROS L2TP server protection. It will help you to block and avoid some malicious connections. To configure this script you have to change ether1-WAN to your WAN interface and put these rules to the first place in your firewall.

**l2tp_protector.src** - The first version of these scripts were made by me almost 5 years ago to protect my L2TP server on Mikrotik Router from brutforce attacks. Now it was rewrited to be able to work on ROS 7.
They constantly checking MT logs for various string like "failed to get valid proposal." and adding IPs to black-list.
To use these scripts you need to add a firewall rules, also you have to add l2tp_protector* schedule. And configure "threshold" variable. Additional description you can find inside every script.

## NAND free space monitoring
**free_space_monitor.src** - This script was made to get an info about NAND free space (/system/resource get free-hdd-space) on Mikrotik ROS v7 and send alerts via email and Telegram when free space is lower than specified threshold.
The main problem is in the fact that some MT routers have too small NAND partition. For example the HEX Router (GR3) with 7.10 ROS firmware has only 2000KB of free space. Is case you use address-lists/DNS/etc heavily, this amount of KB will be filled quite fast. Even if you have 200KB free, it could be filled completely during attempts to clean address-lists/DNS/etc manually.
And in a result there will be 0B free space and ROS will switch to read-only mode. It will work further but unstable and you will not be able to reconfigure, delete something or fix this issue easily.
So there is only one possible way to fix this issue - NetInstall.
After getting in this trouble, I decided to create this script to be able to monitor NAND free space and avoid such issues in a future.
