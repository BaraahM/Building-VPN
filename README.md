# OpenVPN Setup and Configuration

This guide provides step-by-step instructions for setting up an OpenVPN server and configuring a client to connect to it.
## Prerequisites

- A server running a Unix-based operating system (e.g., Ubuntu, macOS).
- OpenVPN and Easy-RSA installed on the server.
- Root or sudo access on the server.
- A client machine to connect to the VPN.

## Step 1: Install OpenVPN and Easy-RSA

### On the Server

1. Install OpenVPN and Easy-RSA:
   ```
   sudo apt update
   sudo apt install openvpn easy-rsa 
2. Set Up the Easy-RSA Environment:
   ```
   make-cadir ~/openvpn-ca
   cd ~/openvpn-ca
   cp /usr/share/easy-rsa/vars.example ./vars 
3. Initialize the PKI::
   ```
   ./easyrsa init-pki
   ./easyrsa build-ca
4. Generate the Server Certificate and Key:
   ```
   ./easyrsa gen-req server nopass
   ./easyrsa sign-req server server
5. itialize the PKI::
   ```
   ./easyrsa gen-dh
   openvpn --genkey --secret ta.key
6. Generate the Server Certificate and Key:
   ```
   sudo cp pki/ca.crt pki/issued/server.crt pki/private/server.key pki/dh.pem ta.key/etc/openvpn

## Step 1: Configure the OpenVPN Server

1. Create the Server Configuration File:
   ```
   sudo nano /etc/openvpn/server.conf
2. Add the Following Configuration to server.conf:
   ```
   port 1194
   proto udp
   dev tun
   ca /etc/openvpn/ca.crt
   cert /etc/openvpn/server.crt
   key /etc/openvpn/server.key
   dh /etc/openvpn/dh.pem
   tls-auth /etc/openvpn/ta.key 0
   cipher AES-256-CBC
   data-ciphers AES-256-GCM:AES-128-GCM:CHACHA20-POLY1305:AES-256-CBC
   topology subnet
   auth SHA256
   server 10.8.0.0 255.255.255.0
   ifconfig-pool-persist ipp.txt
   push "redirect-gateway def1 bypass-dhcp"
   push "dhcp-option DNS 8.8.8.8"
   push "dhcp-option DNS 8.8.4.4"
   keepalive 10 120
   persist-key
   persist-tun
   status openvpn-status.log
   log-append /var/log/openvpn.log
   verb 3

3. Set Correct Permissions:
   ```
   sudo chmod 644 /etc/openvpn/ca.crt
   sudo chmod 644 /etc/openvpn/server.crt
   sudo chmod 600 /etc/openvpn/server.key
   sudo chmod 644 /etc/openvpn/dh.pem
   sudo chmod 600 /etc/openvpn/ta.key
4. Set Correct Permissions:
   ```
   sudo /usr/local/sbin/openvpn --config /etc/openvpn/server.conf --daemon
5. Verify the Server is Running:
   ```
   ps aux | grep openvpn
6. Set Correct Permissions:
   ```
   sudo tail -f /var/log/openvpn.log

   
