# OpenVPN Setup and Configuration

This guide provides step-by-step instructions for setting up an OpenVPN server and configuring a client to connect to it.
https://github.com/BaraahM/Building-VPN/blob/main/README.md
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
   sudo apt install openvpn easy-rsa ```
2.Install OpenVPN and Easy-RSA:
    ```
   make-cadir ~/openvpn-ca
   cd ~/openvpn-ca
   cp /usr/share/easy-rsa/vars.example ./vars ```

   
