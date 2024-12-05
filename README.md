# Setup Instructions
The following instructions are for Windows systems only.

## Docker 
For Windows:

1. **Install Docker Desktop:**
   - Download Docker Desktop for Windows from the [official Docker website](https://docs.docker.com/desktop/setup/install/windows-install/).
   - Run the installer and follow the on-screen instructions.
   - During installation, Docker may prompt you to enable the Windows Subsystem for Linux (WSL) 2 feature. If so, follow the prompts to install and set up WSL 2. If not, check the next sections. 

2. **Verify Installation:**
   - After installation, launch Docker Desktop.
   - Open a Command Prompt or PowerShell window and run:
        ```bash
        docker --version
        ```
   - This command should display the installed Docker version, confirming a successful installation.
        ```bash
        Docker version 27.3.1, build ce12230
        ```

## WSL-2

1. **Enable WSL:**
   - Open PowerShell as an administrator and run:
     ```powershell
     dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
     ```

2. **Enable Virtual Machine Platform:**
   - In the same PowerShell window, run:
     ```powershell
     dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
     ```

3. **Restart Your Computer:**
   - After enabling these features, restart your system to apply the changes.

4. **Set WSL 2 as Default Version:**
   - After restarting, open PowerShell and set WSL 2 as the default version:
     ```powershell
     wsl --set-default-version 2
     ```

5. **Install a Linux Distribution:**
   - Visit the Microsoft Store and install your preferred Linux distribution, e.g. Ubuntu.
   - Launch the installed distribution and complete the initial setup.
   - It'll ask you to setup a new UNIX username and password (and retype the password).

    ***Note***: when typing the password, the password will NOT appear (not even **).

## Docker & WSL 2

1. **Open Docker Desktop:**
   - Launch Docker Desktop from the Start menu.

2. **Access Settings:**
   - Click on the Docker icon in the system tray, then select "Settings."

3. **Enable WSL 2 Backend:**
   - In the "General" tab, ensure that "Use the WSL 2 based engine" is checked.

4. **Integrate with WSL 2 Distributions:**
   - Navigate to "Resources" > "WSL Integration."
   - Enable Docker integration with your installed WSL 2 distributions by toggling the switch next to each distribution.

5. **Apply and Restart:**
   - Click "Apply & Restart" to apply the changes.

## VS-Code
There are some useful extentions:
- WSL, by Microsoft.
- Docker, by Microsoft.
- Dev Containers, by Microsoft.

## Setup Dev Container
Dev Containers ensure a consistent development environment across different setups.

- **Initialize the Dev Container Configuration:**
  - Open your project folder in VS Code.
  - Press `Ctrl+Shift+P` to open the Command Palette.
  - Type `Dev Containers: Add Dev Container Configuration Files` and select it.
  - Choose the following configuration:
      - Add to workspace. 
      - Python 3.
      - 3.12 bullseye (default).
      - Skip to the end (do not add other feautures).

- **Customize the Configuration:**
  - A `.devcontainer` folder will be created in your project directory, containing `devcontainer.json` and possibly a `Dockerfile`.
  - Modify these files to specify the necessary tools, extensions, and settings for your project.

- **Reopen in Container:**
  - After configuring, press `Ctrl+Shift+P` and select `Dev Containers: Reopen in Container`.
  - VS Code will build the Docker container as per your configuration and reopen the project within this environment.

**4. Install Necessary Python Packages:**

With your virtual environment activated, install the required packages.

- **Install Client Libraries:**
  - In the integrated terminal of VS Code, run:
    ```bash
    pip install pymilvus qdrant-client
    ```

# Project's Description
## Comparison between Vector DataBases
In this project, you will be asked to compare the performance of various aspects of two popular and open-source vector database systems (qdrant, milvus). This entails the following aspects that must be tackled by you:

1) Installation and setup of two specific Vector DBs: Using local or okeanos-based resources you are asked to successfully install and setup the two systems. This also means that if any (or both) of the DBs got a cluster edition (distributed mode) that this will be also available for testing.

2) Data generation (or discovery of real data) and loading to the two DBs: Using either a specific data generator, online data or artificially creating data, you should identify and load a significant amount of vectors into the databases. Ideally, loaded data should be:

    a) big (or as big as possible), not able to fit in main memory,

    b) have varying dimensionality (vector size and type - integer, float) and 
    
    c) the same data loaded in both databases.

Data loading is a process that should be monitored, namely: the time it takes to load a small, medium and the final amount of data, as well as the storage space it takes in each of the databases (i.e., how efficient data compression or possible indexing is).

3) Query generation to measure performance: A set of similarity queries (common to both DBs) must be compiled in order to test the performance of the vector DBs. Queries should target similar similarity metric algorithms (if implemented on both DBs, e.g., Euclidean distance (L2), Inner product, Cosine similarity, etc.) with and without filters (https://github.com/qdrant/ann-filtering-benchmark-datasets)

4) Measurement of relevant performance metrics for direct comparison: Client process(es) should pose the queries of the previous step and measure the DB performance (query latency, throughput, CPU load if possible, etc). Teams should be careful and compare meaningful statistics in this important step.

Teams undertaking this project can take advantage of existing benchmarking code either in principle or in whole. I suggest looking at the qdrant Benchmark Suite (https://github.com/qdrant/vector-db-benchmark), which for many of the DBs contains code for data generation, loading, queries and measurement. Besides the aforementioned project aspects, you are free to improvise in order to best demonstrate the relative strengths and weaknesses of each system. By the end of your project, you should have a pretty good idea of what a modern vector DB is, its data and query processing model and convey their strong/weak points.