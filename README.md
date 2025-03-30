# GDS3D Visualization Tutorial for WSL and VcXsrv

## Introduction
This tutorial provides a comprehensive guide for visualizing GDSII layouts in 3D using **GDS3D** on **Windows Subsystem for Linux (WSL)**, with the help of the **VcXsrv** X server. The objective is to demonstrate how to set up the environment, configure necessary tools, and visualize circuit layouts, such as CMOS inverters, in a 3D space.

## Prerequisites

### 1. Install **Windows Subsystem for Linux (WSL)**
WSL allows you to run a Linux distribution alongside your Windows operating system. To install WSL, follow these steps:
- Open **PowerShell** as Administrator and run:
  ```bash
  wsl --install
  ```
- Restart your system if prompted and install your preferred Linux distribution (Ubuntu is recommended).
- More detailed instructions can be found in the [official WSL installation guide](https://docs.microsoft.com/en-us/windows/wsl/install).
  
### 2. Install **VcXsrv (X Server for Windows)**
VcXsrv is required to enable graphical applications to run on Windows from your Linux environment.
- Download and install VcXsrv from [here](https://vcxsrv.com/).
- After installation, run XLaunch and select the following options:
  - **Multiple Windows**
  - **Start no client**
  - **Disable access control**
- Finish the configuration and start the server.

### 3. Install **GDS3D**
GDS3D is the primary tool for 3D visualization of GDSII files. To install it, follow these steps:
1. Clone the GDS3D repository:
    ```bash
    git clone https://github.com/trilomix/GDS3D.git
    cd GDS3D
    ```
2. Build GDS3D:
    ```bash
    mkdir build
    cd build
    cmake ..
    make
    ```
### 4. Install **OpenGL and Other Dependencies**
Ensure you have the necessary libraries to run the graphical interface.
  ```bash
  sudo apt update
  sudo apt install -y libgl1-mesa-glx libglu1-mesa freeglut3
  ```
If you encounter issues with missing libraries, consider updating your system or installing any missing dependencies.

### Setting Up the Environment
1. Configure the `DISPLAY` variable
To enable graphical output from your Linux environment to Windows, set the DISPLAY variable to the IP address of your WSL environment:
    ```bash
    export DISPLAY=172.28.16.1:0
    ```
2. Run **VcXsrv**
Start VcXsrv using XLaunch and keep it running in the background to allow the graphical applications to display on your Windows screen.
3. Test the Configuration
To test if everything is working, run the following command to check if X11 is properly set up:
    ```bash
    xeyes
    ```

### Visualizing a GDS Layout with GDS3D
1. Prepare the GDS and .tech Files
Make sure you have a GDSII layout file and a corresponding `.tech` file. You can find these files in the `examples/` folder of this repository.
2. Run GDS3D
Once your environment is ready, you can visualize the GDS layout in 3D with the following command:
    ```bash
    GDS3D -p ihp_teste.tech -i rfpmos.gds -t TOP
    ```
3. Navigating the 3D Layout
Once the visualization is loaded, use the following controls to interact with the layout:
- Mouse Movement: Rotate the layout.
- Scroll Wheel: Zoom in and out.
- Left/Right Click: Pan the layout.
