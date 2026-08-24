# COIT20261 Network Services and Automation
## Week 03 Tutorial Journal

## Task 1: Simple Application Communications with Netcat

### Aim

The aim of this task was to understand basic application communication using Netcat (`nc`). I also used the network created in the previous tutorial and checked the connectivity between the Linux hosts before working with Netcat.

---

### 1. Checking the Network Configuration

I used the GNS3 project containing four Linux hosts connected through an Ethernet switch.

Before testing communication, I checked the IP configuration of the hosts. The hosts were configured in the `10.1.0.0/24` network.

For example, Host1 was configured with:

```bash
ip addr add 10.1.0.1/24 dev eth0
```

I then checked the configuration using:

```bash
ip a
```

The output confirmed that Host1 had the following IPv4 address:

```text
10.1.0.1/24
```

![Host1 IP Configuration](week03-host1-ip.png)

**Figure 1: Checking the IP configuration of Host1.**

---

### 2. Testing Connectivity Between the Hosts

Before using Netcat, I tested whether Host1 could communicate with the other hosts on the LAN.

From Host1, I first tested Host2 using:

```bash
ping -c 3 10.1.0.2
```

The result showed:

```text
3 packets transmitted, 3 received, 0% packet loss
```

I then tested Host3:

```bash
ping -c 3 10.1.0.3
```

The result also showed:

```text
3 packets transmitted, 3 received, 0% packet loss
```

Finally, I tested Host4:

```bash
ping -c 3 10.1.0.4
```

Again, all three packets were successfully received.

![Ping Connectivity Test](week-03/week03-ping-hosts.png)
**Figure 2: Testing connectivity from Host1 to the other Linux hosts.**

The successful results confirmed that the hosts could communicate with each other before I continued with application-level communication.

---

### 3. Netcat Client and Server Communication

For this activity, Netcat was used to create simple communication between two Linux hosts.

One host was used as the Netcat server and another host was used as the client.

On the server, Netcat can be started in listening mode using:

```bash
nc -l -p <port-number>
```

The tutorial required a port other than `12345`.

On the client, the connection can be made using:

```bash
nc <server-IP-address> <port-number>
```

After the connection was established, a text message containing my name was sent from the client to the server.

The server could then send my student ID back to the client.

The information exchanged during the activity was:

```text
Name: Rohit
Student ID: 12318349
```

This activity demonstrated that Netcat can provide simple application-level communication between two network devices.

Netcat is different from `ping` because `ping` uses ICMP to check network-level connectivity, while Netcat can use TCP or UDP for application communication.

---

## Task 2: Capturing Packets

### Aim

The aim of this task was to capture network packets travelling across a GNS3 link and save the captured traffic as a `.pcap` file.

---

### 1. Starting the Packet Capture

I started a packet capture on the link between Host1 and the Ethernet switch in GNS3.

The capture was started by right-clicking the required network link and selecting:

```text
Start capture
```

The Ethernet link type was selected and the capture was saved in `.pcap` format.

---

### 2. Generating Ping Traffic

While the packet capture was running, I generated network traffic using `ping`.

From Host1, I sent three ICMP requests to another host using:

```bash
ping -c 3 10.1.0.2
```

The result showed:

```text
3 packets transmitted
3 packets received
0% packet loss
```

This generated ICMP request and reply packets that could be recorded in the packet capture.

---

### 3. Generating Netcat Traffic

Netcat communication was also used while the packet capture was active.

A Netcat connection was established between two hosts and a text message was sent through the connection.

This generated application communication that could also be recorded in the `.pcap` file.

After generating the required traffic, I stopped the packet capture in GNS3.

---

### 4. Checking the Windows Host Network Configuration

I also checked the network configuration of the Windows host using PowerShell.

I entered:

```powershell
Get-NetIPConfiguration
```

The output showed the VirtualBox Host-Only Ethernet Adapter with the IPv4 address:

```text
192.168.56.1
```

It also showed the physical Ethernet interface with the IPv4 address:

```text
10.162.33.49
```

and the default gateway:

```text
10.162.32.1
```

![Windows IP Configuration 1](week-03/week03-windows-ip.png)

**Figure 3: Checking the Windows network configuration using Get-NetIPConfiguration.**

This helped me identify the network interfaces and addresses being used by the Windows host and VirtualBox environment.

---

### 5. Testing Connectivity from Windows

I also used PowerShell to test network connectivity.

The command used was:

```powershell
Test-Connection 10.162.33.135
```

The destination successfully responded to the connection test.

The results showed response times between approximately `1 ms` and `3 ms`.

![Windows Test Connection](week-03/week03-test-connection.png)

**Figure 4: Testing network connectivity using PowerShell Test-Connection.**

This confirmed that the destination device was reachable from the Windows computer.

---

### 6. Saving the Packet Capture

After completing the network communication tests, I stopped the packet capture.

The captured traffic was transferred from the GNS3 environment to the Windows host and saved as a `.pcap` file.

My capture file was:

```text
12318349-ping-netcat.pcap
```

The capture contains the network traffic generated during the ping and Netcat activities.

The `.pcap` file can be opened using Wireshark to inspect the captured packets.

---

## What I Learned

In this week's tutorial, I learned the difference between network-level and application-level communication.

I used `ping` to check whether the Linux hosts could communicate with each other. Receiving all the ping responses with `0% packet loss` confirmed that the IP configuration and basic network connectivity were working correctly.

I also learned how Netcat can be used to establish simple communication between a client and server. Unlike ping, which uses ICMP, Netcat allows messages to be exchanged between applications using a specified port.

The packet capture activity also helped me understand that traffic passing through a network link can be recorded in a `.pcap` file. This file can later be opened in Wireshark for further analysis.

I also practised using PowerShell commands such as `Get-NetIPConfiguration` and `Test-Connection` to check the Windows host's network configuration and connectivity.

Overall, this tutorial helped me understand how different network testing tools can be used together to configure, test and observe network communication.
