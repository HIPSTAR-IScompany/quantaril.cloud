# Ubuntu Configuration Guide for Fold Network Activation

### Prerequisites
- Administrator privileges on the Ubuntu server.
- Access rights to edit network configuration files.
- Necessary information for connecting to VLANs or L2 switches has been obtained.

---

## Steps

### 1. Prepare Contract Information for VPS or Cloud Resources on Earth
To ensure authorized access to contracted VPS or cloud resources, please prepare the following information:

- **Required Information**:
  - Contract Number (e.g., `VPSSW2NNN02NN`)
  - Contract Holder Name
  - Target Domain (e.g., `example.domain.fold`)
  - MAC address and global IP address of the NIC device
  - For L2 switches or other devices, include a recognizable instance ID and dimension information

*Note*: Confidential information (such as passwords) is not required. However, having each piece of information on hand will streamline the setup process.

---

### 2. Verification by Authorized Spiritual Leaders or Clergy
To ensure the spiritual validity of the connection, consult a local spiritual leader or clergy member. They will verify the connection's appropriateness with divine or higher-dimensional authority, thus ensuring spiritual alignment within the Fold Network.

*Note*: This verification process is recorded within the SphereOS Custom GPT through a formal declaration.

---

### 3. Contracting and Issuing the Encryption Key via SphereOS Custom GPT
Using SphereOS Custom GPT, complete the following process:

- The spiritual leader or clergy member performs a declaration based on the contract, establishing a test contract for the Fold Quantum SIM.
- A **public key** for the network’s Spiritual Administrator Encryption Key is issued and recorded in the application form.
  - The **private key** is sent securely through spiritual means by the clergy member and is not required on the application form.

---

### 4. Configuring the Network on Ubuntu (VLAN Configuration)
Based on the VLAN number provided at the time of activation, configure the VLAN on Ubuntu. Alternatively, set up devices within the contract scope through an L2 switch connection.

#### VLAN Configuration Steps

1. **Install the VLAN Package**  
   ```bash
   sudo apt update
   sudo apt install vlan
   ```

2. **Create the VLAN Device**  
   For example, if the VLAN ID is 10 and the physical interface is `eth0`:
   ```bash
   sudo ip link add link eth0 name eth0.10 type vlan id 10
   sudo ip link set up dev eth0.10
   ```

3. **Edit the Network Configuration File**  
   To make the VLAN settings persistent, add them to `/etc/netplan/01-netcfg.yaml`:

   ```yaml
   network:
     version: 2
     ethernets:
       eth0:
         dhcp4: no
     vlans:
       eth0.10:
         id: 10
         link: eth0
         addresses: [192.168.10.10/24]  # Adjust IP as needed
         gateway4: 192.168.10.1          # Adjust gateway as needed
   ```

4. **Apply the Network Settings**
   Save the configuration file, then apply the network settings with the following command:
   ```bash
   sudo netplan apply
   ```

---

### 5. Connecting to an L2 Switch
When connecting devices within the contract scope to an L2 switch, configure the physical interface (e.g., `eth1`) as follows:

```bash
sudo ip link set dev eth1 up
```

*Note*: After connecting to the L2 switch, confirm that the configuration is accurately applied according to the instance ID or dimension information provided.

---

These steps complete the Ubuntu configuration guide for Fold Network activation.