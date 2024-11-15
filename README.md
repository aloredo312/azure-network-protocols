<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Actions and Observations</h2>

<p>
<img width="802" alt="filter_icmp" src="https://github.com/user-attachments/assets/9e7b8245-de06-44bc-9fd2-2a3bf4d6e97a">
</p>
<p>
Open Wireshark and start a new packet capture. To see ICMP traffic, filter for ICMP traffic only. Then you can retrieve the private IP address of the Ubuntu VM (linux-vm) and using powershell ping it from within the Windows 10 VM. You can now see the requests and replies inside of Wireshark.
</p>
<br />

<p>
<img width="970" alt="request_timed_out_wireshark" src="https://github.com/user-attachments/assets/32cd6eb2-7cdb-4367-9982-6ae38e42afcc">
</p>
<p>
To configure a Firewall (Network Security Group) we will initiate a non-stop ping from the Windows 10VM to the Ubuntu VM. Open the Network Security Group your Ubuntu VM is using and add a rule that disables incoming ICMP traffic. Back in the Windows 10 VM, observe the ICMP traffic in Wireshark and the command line Ping activity and you will see that the request times out and there is no reply. To re-enable ICMp traffic just delete the rule that was added in the Network Security Group in the Ubuntu VM.
</p>
<br />

<p>
<img width="1102" alt="observing_ssh_traffic" src="https://github.com/user-attachments/assets/5e34d8e8-7776-4fc1-89e5-cad6eadfbab2">
</p>
<p>
To observe for SSH traffic start a new packet capture in Wireshark. Filter for SSH traffic only. From the Windows 10 VM open Powershell, and type: ssh labuser@(private IP adress). Then type commands into the linux SSH connection to observe SSH traffic spam in Wireshark. Type "exit" and press (enter) to exit the SSH connection.
</p>
<br />

<p>
<img width="1192" alt="observing_dns_traffic" src="https://github.com/user-attachments/assets/8c373785-adf2-4ff9-8d38-9c4ad9bf86f7">
</p>
<p>
To observe DNS traffic, filter for DNS traffic. From the Windows 10 VM in the command line, use nslookup to see what google.com, disney.com, or any website you like and see what their IP addresses are. In Wireshark you can observe the DNS traffic that is being shown.
</p>
<br />

<p>
<img width="1085" alt="observing_rdp" src="https://github.com/user-attachments/assets/e314b393-419d-473d-894b-0996670e6826">
</p>
<p>
To observe RDP traffic, filter for RDP traffic only. For this type "tcp.port == 3389". Back in Wireshark you will see the non-stop spam of traffic
</p>
<br />
