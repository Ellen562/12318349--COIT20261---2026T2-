# Week 1 Portfolio â€“ Introduction to GNS3

**Name:** Ellen Gopali  
**Student ID:** 12318349  
**Unit:** COIT20261  
**Term:** 2026 Term 2

## Aim

The aim of this activity was to become familiar with the basic features of GNS3. I practised creating a project, adding a Linux host, setting a static IP address and checking the address through the host console.

## What I did

I created a GNS3 project named `GNS3-Intro-12318349`. I then added one Linux Host node and placed a text box in the workspace showing the unit code, my name and student ID.

Before starting the host, I configured the `eth0` interface with the static IPv4 address `10.10.1.1` and the subnet mask `255.255.255.0`. This subnet mask is also written as `/24`.

The interface settings used for the activity were:

```text
auto eth0
iface eth0 inet static
address 10.10.1.1
netmask 255.255.255.0
up sysctl net.ipv4.ip_forward=0
```

After saving the configuration, I started Host1 and opened its web console. I entered the following command to view the network interfaces and confirm the IP address:

```bash
ip a
```

The output showed `inet 10.10.1.1/24` under `eth0`, which confirmed that the static IP address had been applied successfully.

## Evidence

### GNS3 project and Linux host

The screenshot below shows my GNS3 project with one Linux Host node and my student details added to the workspace.

![GNS3 project showing Host1 and student details](images/GNS3-Intro-12318349-network.png)

### IP address verification

The next screenshot shows the result of the `ip a` command. The `eth0` interface has the IPv4 address `10.10.1.1/24`.

![Host1 console showing the configured IP address](images/GNS3-Intro-12318349-ipaddress.png)

## What I learned

This activity helped me understand how to create and manage a simple GNS3 project. I learned that the network settings need to be configured before starting this Linux host. I also learned how to use `ip a` to check whether an IP address has been assigned correctly. The `/24` shown in the output represents the subnet mask `255.255.255.0`.

At first, the console output looked difficult because it displayed the loopback interface and the Ethernet interface together. After checking the interface names carefully, I found the required address under `eth0`.

## Result

I completed the basic GNS3 setup successfully. Host1 started correctly, and its `eth0` interface showed the static IP address `10.10.1.1/24`.
