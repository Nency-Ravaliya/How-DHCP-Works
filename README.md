# How DHCP Works?

# DHCP: Dynamic Host Configuration Protocol 

## What is DHCP?
DHCP is a network protocol that automatically assigns IP addresses, subnet masks, gateways, and DNS settings to devices when they connect to a network. This saves you from having to manually configure network settings for each device.

## Scenario
You just connected your laptop to your home Wi-Fi, and now it needs an IP address to communicate with other devices and the internet. Here’s how DHCP works in this case.

## Step-by-Step DHCP Workflow

### DHCP Discover (Laptop → Router)
- **What Happens:** When your laptop connects to the Wi-Fi for the first time, it doesn't have an IP address. So, it sends out a DHCP Discover message to find a DHCP server. This message is sent as a broadcast because your laptop doesn't know its IP yet.
- **Details:**
  - **Layer:** This is a Layer 2 (Data Link) broadcast message because your laptop is trying to find a DHCP server in the local network.
  - **Attributes:** Your laptop’s MAC address is included in the message because it doesn’t have an IP address yet.
  - **Example Message:**
    ```
    DHCP Discover: Who can give me an IP address?
    Source: Laptop's MAC address
    Destination: Broadcast (FF:FF:FF:FF:FF:FF)
    ```

### DHCP Offer (Router → Laptop)
- **What Happens:** The Wi-Fi router (which also acts as the DHCP server in home networks) receives the DHCP Discover message and responds with a DHCP Offer. This message contains an IP address that the router is offering to your laptop, along with the subnet mask, default gateway, and DNS server addresses.
- **Details:**
  - **Layer:** This is a Layer 3 (Network) communication because it involves IP addresses, although it’s still broadcast within the local network.
  - **Attributes:** The offered IP address, subnet mask, gateway IP (the router’s IP), and DNS server IP are included.
  - **Example Message:**
    ```
    DHCP Offer: Here’s an IP address (192.168.1.10) for you.
    Offered IP: 192.168.1.10
    Subnet Mask: 255.255.255.0
    Gateway: 192.168.1.1
    DNS: 8.8.8.8 (Google’s DNS)
    ```

### DHCP Request (Laptop → Router)
- **What Happens:** Your laptop receives the DHCP offer and sends back a DHCP Request message to the router, saying that it would like to use the offered IP address. This is still sent as a broadcast so that all devices on the network are aware of the IP allocation.
- **Details:**
  - **Layer:** This is also a Layer 3 (Network) communication, confirming the IP allocation.
  - **Attributes:** The requested IP address and the laptop’s MAC address are included.
  - **Example Message:**
    ```
    DHCP Request: I’d like to use 192.168.1.10.
    Source: Laptop’s MAC address
    Requested IP: 192.168.1.10
    ```

### DHCP Acknowledgement (Router → Laptop)
- **What Happens:** The router sends back a DHCP Acknowledgement message, confirming that the IP address is now assigned to your laptop. It also provides additional configuration, such as the lease time (how long the IP address will be valid) and the DNS server IP addresses.
- **Details:**
  - **Layer:** This is a Layer 3 (Network) communication. Now your laptop has a valid IP and can start communicating with the network and the internet.
  - **Attributes:** The confirmed IP address, lease time, and DNS configuration.
  - **Example Message:**
    ```
    DHCP ACK: You’re good to go with 192.168.1.10.
    Lease Time: 24 hours
    DNS: 8.8.8.8
    ```

## DHCP Parameters Provided
When the DHCP Acknowledgment is sent from the router, it provides the following information to your laptop:
- **IP Address:** E.g., 192.168.1.10 (the local IP for your laptop).
- **Subnet Mask:** E.g., 255.255.255.0 (defines the size of your local network).
- **Default Gateway:** E.g., 192.168.1.1 (this is usually your router’s IP, which is your laptop’s way out to the internet).
- **DNS Server IP:** E.g., 8.8.8.8 (Google’s DNS server that will translate domain names like google.com into IP addresses).
- **Lease Time:** E.g., 24 hours (after this time, the laptop will need to renew the lease and get a new or the same IP).

![image](https://github.com/user-attachments/assets/08c7653f-b674-495d-86ba-d66d9c926b6b)

## How DHCP Relates to OSI Layers

Here’s a quick look at how DHCP fits into the OSI model:
- **Layer 1 (Physical Layer):** DHCP requests and responses travel over physical connections (like Ethernet or Wi-Fi).
- **Layer 2 (Data Link Layer):** Initially, your laptop only knows its MAC address and uses it to communicate on the network.
- **Layer 3 (Network Layer):** DHCP assigns an IP address, subnet mask, and gateway IP for Layer 3 communication. After this, your laptop can talk to devices on the network and access the internet.
- **Layer 7 (Application Layer):** DHCP itself is a protocol running at the application layer, which provides the service of automatic IP configuration.

## Example Timeline of Events
1. You turn on your laptop and connect to Wi-Fi. Your laptop sends a DHCP Discover message because it doesn’t have an IP address.
2. The router receives the request and offers an IP (e.g., 192.168.1.10) through a DHCP Offer.
3. Your laptop accepts this IP by sending a DHCP Request.
4. The router confirms with a DHCP Acknowledgment that the IP is assigned, along with other details like the subnet mask, gateway, and DNS.
5. Now your laptop can communicate on the network, access the internet, and resolve domain names (like google.com) to IP addresses using the DNS server.

## Key DHCP Concepts:
- **Dynamic IP Assignment:** DHCP dynamically assigns IP addresses from a pool (e.g., 192.168.1.2 - 192.168.1.254). No need to manually configure IPs for each device.
- **Lease Time:** DHCP assigns IPs for a specific duration. After the lease expires, the device must request a renewal or a new IP.
- **Broadcasting:** Initially, DHCP messages (Discover and Request) are sent as broadcasts because the device doesn't know its own IP or the IP of the DHCP server.

## Summary
- DHCP automatically assigns IP addresses, subnets, gateways, and DNS settings to devices when they join a network.
- In your home network, your router acts as the DHCP server.
- The DHCP process includes four main steps: Discover, Offer, Request, and Acknowledge.
- After the DHCP process, your laptop has all the network configurations needed to communicate with other devices and access the internet.
