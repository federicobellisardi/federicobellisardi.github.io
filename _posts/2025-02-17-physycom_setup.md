---
title: "Prerequisites for Mobilis Code Building"
description: >-
  A comprehensive guide to setting up a modern development environment across Ubuntu (including WSL), macOS, Windows, and Cygwin.
  This updated guide covers installation instructions, environment setup, and necessary tools to build code efficiently on various platforms.
author: fbellisardi
date: 2025-02-21 14:00:00 +0100
categories: [Blogging, Tutorial]
tags: [getting_started, development, environment_setup]
pin: true
---

# Prerequisites for Mobilis Code Building

This guide provides detailed instructions to set up the development environment for building and deploying **Mobilis**, a C++ simulator developed at the **City Science Lab** of the **University of Bologna**. **Mobilis** is used to simulate traffic flows in a graph, and it requires specific tools and configurations to function correctly.

The following steps outline how to configure your development environment on various platforms, including **Ubuntu** (with or without WSL on Windows), **macOS**, **Windows (10/11)**, and **Cygwin**. These instructions ensure that all necessary tools and dependencies are installed so that you can efficiently build and deploy **Mobilis** on your machine.

Follow the steps for your platform to get started with the simulation project.


---

## Ubuntu on Windows (WSL)

For users running Ubuntu via Windows Subsystem for Linux (WSL) on Windows 10/11, follow these steps:

1. **Install and Update WSL:**
   - Ensure you have WSL 2 installed. If not, follow the official [Microsoft WSL installation guide](https://docs.microsoft.com/en-us/windows/wsl/install).

2. **Install Chocolatey (if not already installed):**
   - Refer to [Chocolatey.org](https://chocolatey.org) for installation instructions.

3. **Install an X Server (for GUI applications):**
   - **Windows 10:** Install [VcXsrv](https://sourceforge.net/projects/vcxsrv/) using Chocolatey. Open PowerShell as Administrator and run:
      ```PowerShell
      cinst -y vcxsrv
      ```
   - **Windows 11:** WSLg supports Linux GUI applications natively, so an external X server is typically not required.

4. **Launch the X Server:**
   - If using VcXsrv, run it and keep it open whenever you need graphical support in WSL.

5. **Configure the DISPLAY Variable:**
   - In your Ubuntu (WSL) terminal, add the following to your `~/.bashrc` (or `~/.zshrc` if using Zsh):
     ```bash
     echo -e "\nexport DISPLAY=localhost:0.0\n" >> ~/.bashrc
     source ~/.bashrc
     ```

6. **Proceed with the Ubuntu setup below.**

---

## Ubuntu

1. **Create a Workspace Directory:**
   - Define a work folder (e.g., `~/code` or another preferred location). Note its full path (e.g., `/home/yourusername/code`).

2. **Set the WORKSPACE Environment Variable:**
   - Open a terminal and run (replace `/full/path/to/my/folder` with your folder's full path):
      ```bash
      echo -e "\nexport WORKSPACE=/full/path/to/my/folder\n" >> ~/.bashrc
      source ~/.bashrc
      ```

3. **Update Your System:**
  ```bash
   sudo apt-get update
   sudo apt-get dist-upgrade
  ```

4. **Install Essential Development Tools and Libraries:**
  ```bash
    sudo apt-get install -y g++ cmake make git dos2unix ninja-build
    git config --global core.autocrlf input
    git clone https://github.com/physycom/sysconfig
    sudo apt-get install -y libboost-all-dev libfltk1.3-dev freeglut3-dev libgl1-mesa-dev libglu1-mesa-dev libxinerama-dev libjpeg-dev libxi-dev libxmu-dev libcurl4-openssl-dev
  ```
5. **Verify and Update CMake (if necessary):**

  - Check the installed version:
    ```bash
    cmake --version
    ```
  - If the version is older than 3.20, consider installing a newer version. For example, for Linux 64-bit:
    ```bash
    cd $WORKSPACE
    export CMAKE_FULL_VERSION="cmake-3.27.0-Linux-x86_64"
    export CMAKE_VERSION="v3.27"
    mkdir -p cmake
    cd cmake
    wget https://cmake.org/files/${CMAKE_VERSION}/${CMAKE_FULL_VERSION}.tar.gz
    tar zxvf ${CMAKE_FULL_VERSION}.tar.gz
    echo -e "\nexport PATH=${WORKSPACE}/cmake/${CMAKE_FULL_VERSION}/bin:\$PATH\n" >> ~/.bashrc
    source ~/.bashrc
    ```

6. **Your Ubuntu environment is now ready for code building.**

## macOS

1. **Install Xcode Command Line Tools:**
  ```bash
  xcode-select --install
  ```
2. **Install Homebrew (if not already installed):**
    - Follow the instructions on the [Homebrew website](https://brew.sh/).

3. **Update Homebrew and Install Required Packages:**
  ```bash
  brew update && brew upgrade
  brew install cmake make git dos2unix ninja
  git config --global core.autocrlf input
  git clone https://github.com/physycom/sysconfig
  brew install fltk boost freeglut
  ```
4. **Create a Workspace Directory:**
    - Define your workspace (e.g., `~/code`).

5. **Set the WORKSPACE Environment Variable:**
    - Open Terminal and run (replace `/full/path/to/my/folder` with your workspace path):
        ```bash
        echo -e "\nexport WORKSPACE=/full/path/to/my/folder\n" >> ~/.bash_profile
        source ~/.bash_profile
        ```

## Windows (10/11)
1. Install Visual Studio:
  - Install or update to [Visual Studio](https://visualstudio.microsoft.com/vs/community). Ensure it is fully updated.

2. Install Chocolatey (if not already installed):
  - Follow the instructions on [Chocolatey.org](https://chocolatey.org).

3. Install Required Tools via Chocolatey:
  - Open `PowerShell` with Administrator privileges and run:
      ```powershell
        cinst -y git cmake powershell ninja
      ```
  - Restart your PC if prompted.

4. Set PowerShell Execution Policy:
  - In an Administrator PowerShell, run:
    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```
5. Create a Workspace Directory:
  - Create a folder for your code (e.g., `C:\Code`).

6. Configure Environment Variables:
  - Open a standard user PowerShell and run:
    ```powershell
    rundll32 sysdm.cpl,EditEnvironmentVariables
    ```
  - Add or update the following variables:
    ```
      WORKSPACE → full path of your workspace.
      VCPKG_ROOT → %WORKSPACE%\vcpkg
      VCPKG_DEFAULT_TRIPLET → x64-windows-physycom
    ```
  - Ensure the following is added to your PATH:
    ```powershell
        %PROGRAMFILES%\CMake\bin
    ```

7. Clone the sysconfig Repository:
  - In a standard user PowerShell, run:
    ```powershell
    cd $env:WORKSPACE
    git config --global core.autocrlf input
    git clone https://github.com/physycom/sysconfig.git
    ```
8. Install vcpkg (if not already installed):
    ```powershell
    cd $env:WORKSPACE
    git clone https://github.com/Microsoft/vcpkg.git
    cd vcpkg
    cp ..\sysconfig\cmake\x64-windows-physycom.cmake .\triplets\
    .\bootstrap-vcpkg.bat
    ```

9. Integrate vcpkg with Visual Studio:
  - Open an Administrator PowerShell and run:
    ```powershell
    cd $env:WORKSPACE\vcpkg
    .\vcpkg integrate install
    ```
10. Install Necessary Libraries via vcpkg:
  - In a standard user PowerShell, run:
    ```powershell
    cd $env:WORKSPACE\vcpkg
    .\vcpkg install fltk fltk:x86-windows-static boost boost:x86-windows-static freeglut freeglut:x86-windows-static opengl opengl:x86-windows-static
    rmdir .\buildtrees\ /s /q
    ```
11. Update Software:
  - To update Chocolatey packages, open an Administrator PowerShell and run:
      ```powershell
      cup all -y
      ```

  - To update libraries in vcpkg:
      ```powershell
      cd $env:WORKSPACE\vcpkg
      git pull
      .\bootstrap-vcpkg.bat
      .\vcpkg update
      .\vcpkg upgrade --no-dry-run
      ```
## Cygwin

1. Install Chocolatey (if not already installed):
  - Follow the instructions on Chocolatey.org.

2. Install Cygwin via Chocolatey:
  - Open PowerShell with Administrator privileges and run:
      ```powershell
      cinst -y cygwin
      ```
3. Create a Workspace Directory:
  - Create a folder for your code (e.g., `C:\Code`).

4. Set the WORKSPACE Environment Variable:
  - Open a standard user PowerShell and run:
    ```powershell
    rundll32 sysdm.cpl,EditEnvironmentVariables
    ```
  - Add a new variable named `WORKSPACE` with the full path of your workspace.

5. Install Required Cygwin Packages:

  - Open a standard user PowerShell, navigate to your workspace, and run:
    ```powershell
    cd $env:WORKSPACE
    Invoke-WebRequest https://cygwin.com/setup-x86_64.exe -OutFile $env:WORKSPACE\cygwin-setup.exe
    .\cygwin-setup.exe --quiet-mode --no-shortcuts --no-startmenu --no-desktop --upgrade-also --packages gcc-g++,cmake,git,dos2unix,libboost-devel,libfltk-devel,libglut-devel,libGL-devel,libGLU-devel,fluid,libjpeg-devel,libXi-devel,libXmu-devel
    git clone https://github.com/physycom/sysconfig.git
    ```