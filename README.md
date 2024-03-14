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

<h2>Operating Systems Used</h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04


<h2>High-Level Steps</h2>

<ul>
  <li>Setup Virtual Machines in Azure</li>
  <li>Observe ICMP Traffic</li>
  <li>Observe SSH Traffic</li>
  <li>Observe DHCP Traffic</li>
  <li>Observe DNS Traffic</li>
  <li>Observe RDP Traffic</li>
</ul>

<h2>Actions and Observations</h2>

<b>Setup Virtual Machines in Azure</b>
<ol>
  <li>Create a Resource Group</li>
  <li>On Azure, create the first VM as a Windows 10 PC
    <ul>
      <li>Use the previously created Resource Group</li>
    </ul>
  </li>
  <li>Create the second VM and setup as an Ubuntu server
    <ul>
      <li><b>NOTE: Use the same Resource Group and Vnet created for both VMs.</b></li>
    </ul>
  </li>
</ol>
<p>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/edc3eb20-5878-4eb3-a21f-87e89795625a" height="45%" width="45%" alt="Windows VM created"/>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/67449610-48ee-46e6-9bf3-ac43fc9e0cf4" height="45%" width="45%" alt="Ubuntu server VM created"/>
</p>
<br />


<b>Observe ICMP Traffic</b>
<ol>
  <li>Use Remote Desktop to connect to your Windows 10 Virtual Machine</li>
  <li>Within your Windows 10 Virtual Machine, install Wireshark</li>
  <li>Open Wireshark and filter for ICMP traffic only</li>
  <li>Retrieve the private IP address of the Ubuntu VM and initiate a non-stop ping from your Windows 10 VM
    <ul>
      <li>Observe ping requests and replies within WireShark</li>
    </ul>
  </li>
  <li>Open the <b>Network Security Group</b> your Ubuntu VM is using in Azure Portal and disable inbound ICMP traffic
    <ul>
      <li>Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity</li>
    </ul>
  </li>
  <li>Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using
    <ul>
      <li>Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)</li>
    </ul>
  </li>
</ol>
<p>
<p>Inbound ICMP traffic disabled</p>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/9c859bd8-e042-425c-941f-8d03300df82a" height="45%" width="45%" alt="Disabled Inbound ICMP on Azure"/>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/bed6e687-f165-4ce8-b707-129f2aa36625" height="45%" width="45%" alt="Ping response after disabling ICMP traffic"/>
<p>Inbound ICMP traffic enabled</p>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/bc52d1e3-d250-402e-8114-074839f099bb" height="45%" width="45%" alt="Enabled Inbound ICMP on Azure"/>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/eb76c94c-7763-4982-995c-1a23a9894013" height="45%" width="45%" alt="Ping response after enabling ICMP traffic"/>
</p>
<br />



<b>Observe SSH Traffic</b>
<ol>
  <li>In Wireshark, filter for SSH traffic only</li>
  <li>From the Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
    <ul>
      <li>Type some commands (hostname, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark</li>
    </ul>
  </li>
</ol>
<p>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/91ba0a5b-580a-4769-bfc8-79344dd041af" height="90%" width="90%" alt="Wireshark and CMD line view of SSH traffic"/>
</p>
<br />



<b>Observe DHCP Traffic</b>
<ol>
  <li>In Wireshark, filter for DHCP traffic only</li>
  <li>From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
    <ul>
      <li>Observe the DHCP traffic appearing in WireShark</li>
    </ul>
  </li>
</ol>
<p>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/b5211b08-188f-4b8c-9878-72510fafda73" height="90%" width="90%" alt="Wireshark view of DHCP traffic"/>
</p>
<br />



<b>Observe DNS Traffic</b>
<ol>
  <li>In Wireshark, filter for DNS traffic only</li>
  <li>From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
    <ul>
      <li>Observe the DNS traffic shown in WireShark</li>
    </ul>
  </li>
</ol>
<p>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/5037c369-e424-451f-b2e0-7da152041832" height="90%" width="90%" alt="Wireshark view of DNS traffic"/>
</p>
<br />


<b>Observe RDP Traffic</b>
<ol>
  <li>In Wireshark, filter for RDP traffic only (tcp.port == 3389)</li>
  <li>Observe the surge of RDP traffic shown in WireShark</li>
</ol>
<p>
<img src="https://github.com/tomie-s/azure-nsgs/assets/59409588/a6e90dfb-de63-4d62-83df-16a8a0233361" height="90%" width="90%" alt="Wireshark view of DNS traffic"/>
</p>
<br />

