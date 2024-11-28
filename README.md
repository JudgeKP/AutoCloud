Here is a formal write-up of the steps to set up CARLA on a Windows environment:

---

# Setting Up CARLA Simulator in Windows with Unreal Engine 4.26.2

This guide outlines the steps to set up the CARLA simulator using Unreal Engine 4.26.2 (modified CARLA fork) in a Windows environment. For additional reference, consult this [video tutorial](https://www.youtube.com/watch?v=lLkFA0fPrgs&t=4205s).

### Prerequisites

1. **Install Python 3.8.10**  
   Ensure Python 3.8.10 is installed along with the following dependencies:
   ```bash
   pip3 install --user setuptools
   pip3 install --user wheel
   ```
2. **Install Visual Studio 2022 (Community Edition)**  
   - Include necessary libraries like **Desktop Development with C++** and **.NET Framework Build Tools**, following the CARLA setup manual.

3. **Install Additional Tools**  
   - **CMake 3.31.0**
   - **GNU Make 3.81 (GnuWin32)**
   - **7-Zip Installer**
   - **Git 2.45.2**

   Add the paths of these tools to the environment variables with high priority.

4. **Address Common Issues**  
   - **Out of Heap Memory Issue:** Increase the page swap file size in system settings.  
   - **Long Path Errors:** If the path to Visual Studio Code is too long, configure it in the command line using a function that sets the path to VS Code.

---

### Setup GitHub and Unreal Engine Accounts

1. Create a **GitHub account** and generate a **classic token**.  
2. Create an **Unreal Engine account** with the same email and link it to your GitHub account.  

---

### Environment Configuration

1. **Work within a Python Virtual Environment**  
   Run all commands in a virtual environment using Command Prompt with administrator permissions.

2. **Prepare Unreal Engine Directory**  
   Create a folder named `UnrealEngine` outside the CARLA directory. Set the environment variable as follows:  
   - **Variable Name:** `UE4_ROOT`  
   - **Value:** Path to the `UnrealEngine` folder  

3. **Clone the Unreal Engine Repository**  
   Run the following commands to clone the CARLA-modified Unreal Engine fork:  
   ```bash
   git clone --depth 1 -b carla https://<github_token>@github.com/CarlaUnreal/UnrealEngine.git .
   git reset --hard "4da0c74"
   ```

4. **Set Up Unreal Engine**  
   Navigate to the Unreal Engine root folder and execute:  
   ```bash
   Setup.bat
   GenerateProjectFiles.bat
   ```  
   Refer to [this guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/building-unreal-engine-from-source?application_version=5.4) for building Unreal Engine successfully.

5. **Verify Unreal Engine Installation**  
   After building, navigate to `UnrealEngine\Engine\Binaries\Win64\` and run `UE4Editor.exe`.  
   If a DirectX 11 error occurs, modify the project settings to use DirectX 12 as specified in the Unreal Engine issue page.

---

### Building CARLA

1. **Clone the CARLA Repository**  
   ```bash
   git clone https://github.com/carla-simulator/carla
   ```

2. **Download CARLA Content**  
   Execute:  
   ```bash
   Update.bat
   ```

3. **Build CARLA**  
   Open the **x64 Native Tools Command Prompt for VS 2022** in administrator mode and run:  
   ```bash
   make PythonAPI GENERATOR="Visual Studio 17 2022"
   make launch GENERATOR="Visual Studio 17 2022"
   ```  
   When Unreal Engine opens, press the **Launch** button to verify successful operation.

---

### Final Steps and PythonAPI Examples

1. Navigate to the examples directory:  
   ```bash
   cd carla\PythonAPI\examples
   ```

2. Install Python dependencies:  
   ```bash
   pip install -r requirements.txt
   pip install networkx
   ```

---

### Common Errors

1. **RPC Bind Error**  
   If port 8000 is in use, check with the command:  
   ```bash
   netstat -aon | findstr :8000
   ```  
   Kill the task using the process ID (PID):  
   ```bash
   taskkill /PID <PID> /F
   ```  

By following these steps, CARLA should be successfully installed and running on your system.
