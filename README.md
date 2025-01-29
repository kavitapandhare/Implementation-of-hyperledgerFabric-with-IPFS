
# Implementing Hyperledger Fabric and IPFS for Secure Data Sharing: Complete Setup and Troubleshooting
This guide covers the step-by-step process of setting up Hyperledger Fabric on both Linux-based environments and Windows using WSL2 with Docker, along with troubleshooting common errors that can occur during setup.


## Project Directory Structure

```plaintext
fabric-project/
├── fabric-samples/
│   ├── bin/
│   ├── config/
│   ├── test-network/
│   └── asset-transfer-basic/
├── ipfs/
│   ├── nodejs-project/
├── docker-compose.yaml
└── README.md
```

## Prerequisites

Before getting started with the setup, ensure the following prerequisites are installed:

### 1. **Docker Desktop**
   - Docker must be installed and running for the setup to work.
   - For Windows, ensure Docker Desktop is using **WSL 2** backend.

### 2. **WSL 2 (Windows Subsystem for Linux 2)**
   - WSL 2 is required for the Docker setup to work seamlessly in Windows.

### 3. **Node.js** 
   - Node.js is required for interacting with the IPFS network.

### 4. **IPFS** 
   - IPFS is used for decentralized file storage.

## Installation Steps for Prerequisites

### 1. **Install Docker Desktop**
   - **Windows**:
     - Download Docker Desktop from [here](https://www.docker.com/products/docker-desktop).
     - During installation, ensure the **WSL 2** option is selected.
     - After installation, run Docker Desktop and enable **WSL 2** in Docker Desktop settings.
     - Enable WSL 2 backend in Docker Desktop:
       - Open Docker Desktop → Settings → General → **Use the WSL 2 based engine**.
     - Restart Docker Desktop after enabling WSL 2.
   
   - **Linux**:
     - For Linux-based systems, follow [Docker's Linux installation guide](https://docs.docker.com/engine/install/).

### 2. **Install WSL 2 (for Windows)**
   - Ensure you have Windows 10 or later.
   - Install WSL 2 by following the steps from [Microsoft's WSL installation guide](https://docs.microsoft.com/en-us/windows/wsl/install).
   - Use the following commands to install WSL 2 and set Ubuntu as your default distribution:
     ```bash
     wsl --set-default-version 2
     wsl --install -d Ubuntu
     ```

### 3. **Install Node.js**
   - **Windows and Linux**:
     - Visit the official Node.js website [here](https://nodejs.org) and download the LTS version.
     - Alternatively, on Linux, use the following commands:
       ```bash
       sudo apt update
       sudo apt install nodejs npm
       ```

### 4. **Install IPFS**
   - **Windows**:
     - Download and install IPFS from [here](https://dist.ipfs.io/go-ipfs/v0.14.0/go-ipfs_v0.14.0_windows-amd64.zip).
     - Extract the zip and add the extracted folder to your PATH environment variable.
   
   - **Linux**:
     - Install IPFS using the following commands:
       ```bash
       wget https://dist.ipfs.io/go-ipfs/v0.14.0/go-ipfs_v0.14.0_linux-amd64.tar.gz
       tar -xvzf go-ipfs_v0.14.0_linux-amd64.tar.gz
       cd go-ipfs
       sudo bash install.sh
       ```

## Hyperledger Fabric Setup

### Step 1: **Clone Hyperledger Fabric Samples**
   - Clone the Hyperledger Fabric samples from the official repository:
   ```bash
   git clone https://github.com/hyperledger/fabric-samples.git
   cd fabric-samples
   ```

### Step 2: **Download Fabric Binaries**
   - Download the necessary Fabric binaries (if not already downloaded):
   ```bash
   curl -sSL https://bit.ly/2ysbOFE | bash -s
   ```

### Step 3: **Start the Network**
   - Navigate to the `test-network` folder and start the network:
   ```bash
   cd test-network
   ./network.sh up createChannel -c mychannel -ca
   ```

### Step 4: **Verify the Network**
   - Check the status of the channel:
   ```bash
   ./network.sh channelList
   ```

### Step 5: **Deploy the Chaincode**
   - Deploy the chaincode (e.g., asset transfer chaincode) to the network:
   ```bash
   ./network.sh deployCC -ccn basic -ccp ../asset-transfer-basic/chaincode-go -ccl go
   ```

## IPFS Integration

### Step 1: **Setting Up the IPFS Network**
   - Create a folder for your IPFS project and navigate into it.
   - Initialize the IPFS node:
   ```bash
   ipfs init
   ```

### Step 2: **Running IPFS Node**
   - Start the IPFS node:
   ```bash
   ipfs daemon
   ```

### Step 3: **Adding Files to IPFS**
   - You can add files to the IPFS network using the following command:
   ```bash
   ipfs add <filename>
   ```

### Step 4: **Interfacing Fabric with IPFS**
   - In your chaincode, integrate the functionality to store files on IPFS by adding their hashes to the blockchain.

## Troubleshooting

### 1. **Error: `peer channel list` Command Fails**
   - **Cause**: Missing core.yaml or MSP directories.
   - **Solution**: Ensure the correct path to the MSP directory and core.yaml file is set in your Fabric configuration. You might need to adjust the `CORE_PEER_MSPCONFIGPATH` and `CORE_PEER_LOCALMSPID` environment variables.

### 2. **Error: `cannot connect to Docker daemon`**
   - **Cause**: Docker is not running or not configured to use WSL 2.
   - **Solution**: Ensure Docker Desktop is running with WSL 2 enabled. Restart Docker Desktop and check that WSL 2 is selected.

### 3. **Error: `Channel already exists`**
   - **Cause**: The channel you are trying to create already exists.
   - **Solution**: Use `peer channel delete` to delete the existing channel or use a different channel name for creation.

### 4. **Error: `docker-compose` Command Fails**
   - **Cause**: Incorrect Docker configuration or missing Docker images.
   - **Solution**: Ensure the Docker images are correctly pulled and Docker is configured with WSL 2 as the backend. Restart Docker if needed.

---

This guide provides a comprehensive step-by-step approach to set up and troubleshoot Hyperledger Fabric with IPFS integration in both Linux and Windows environments (with WSL 2).
This `README.md` contains a clear project directory structure, prerequisites, and installation steps for all necessary tools (including Docker, WSL 2, Node.js, and IPFS). It also includes the process of setting up Hyperledger Fabric, IPFS integration, and troubleshooting common issues.

