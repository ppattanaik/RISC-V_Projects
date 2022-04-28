## Setting up the Platform:

### Installing WSL 2(Optional):
- ***Note: If you already have Ubuntu OS, then skip this step and directly proceed to ['Installing Bluespec Compiler'](https://github.com/ppattanaik/RISC-V_Projects/tree/main/Shakti_On_Artix-7/Installations#installing-bluespec-compiler)***

Open Windows powershell as administrator and execute the following commands:

- ***Enable WSL2***

```dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart```
- ***Enable 'Virtual Machine Platform'***

For Windows 10(2004 or above):

``` dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart```

For Windows 10(1903,1909):

 ```Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform -NoRestart```
- ***Restart Computer***
- [***Download the Linux kernel update package*** ](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)
- ***Run the update package downloaded in the previous step. (Double-click to run - you will be prompted for elevated permissions, select ‘yes’ to approve this installation.)***
- ***Set WSL 2 as default***

 ```wsl --set-default-version  2```
- ***Install your Linux distribution***

[Ubuntu 16.04 LTS](https://www.microsoft.com/store/apps/9pjn388hp8c9)

[Ubuntu 18.04 LTS](https://www.microsoft.com/store/apps/9N9TNGVNDL3Q)(Recommended)

[Ubuntu 20.04 LTS](https://www.microsoft.com/store/apps/9n6svws3rx71)
- ***Open Ubuntu And update***
```
 sudo apt-get update
 ```
```
 sudo apt-get upgrade
 ```
 ```
 sudo apt-get dist-upgrade
```
- ***Note:***
``` bash
Installing, this may take a few minutes...
WslRegisterDistribution failed with error: 0x8007019e
The Windows Subsystem for Linux optional component is not enabled. Please enable it and try again.
See https://aka.ms/wslinstall for details.
Press any key to continue...
```
##### ***After opening Ubuntu, if this error appears, reinstall the Linux kernel update package***
- ***Switch Between WSL1 and WSL2***

To switch  `Ubuntu`  to WSL1, enter:
```
wsl --set-version Ubuntu 1
```
To switch  `Ubuntu`  to WSL2, enter:
```
wsl --set-version Ubuntu 2
```
### [](https://github.com/ppattanaik/RISC-V_Projects/tree/main/Shakti_On_Artix-7/Installations#installing-bluespec-compiler)Installing Bluespec Compiler
- ***Installing software dependaencies***

Ensure a stable internet connection (Use unprotected networks, preferably Mobile Hotspots).
Move to the Home folder and run the following commands:
```
cd
```
```
sudo apt install ghc libghc-regex-compat-dev libghc-syb-dev iverilog
```
```
sudo apt install libghc-old-time-dev libfontconfig1-dev libx11-dev
``` 
```
sudo apt install libghc-split-dev libxft-dev flex bison libxft-dev 
```
```
sudo apt install tcl-dev tk-dev libfontconfig1-dev libx11-dev gperf
``` 
```
sudo apt install itcl3-dev itk3-dev autoconf git
```
- ***Cloning the Bluespec Repository***

Move to the Home directory and download the repository:
```
cd
```
```
git clone --recursive https://github.com/B-Lang-org/bsc 
```
```
cd bsc 
```
Provide the path to the folder to which bluespec has to be installed:
```
make PREFIX=/path/to/installation/folder 
```
Example:
```
make PREFIX=/home/punya/test 
```

Move to the home directory and open bashrc
```
cd
```
```
vi .bashrc
```
Add the bluespec path to the .bashrc file and save it
```
export PATH=$PATH:/path/to/installation/folder/bin 
```
Example
```
make PREFIX=/home/punya/test/bin
```
• To check if bluespec is installed, open a new terminal and type the following command:
```
bsc -help
```
##### ***> If various commands of Bluespec compiler are displayed, then Bluespec is successfully installed*** 

### Installing Device Tree Compiler
Move to the Home folder and run the following commands:
```
cd
```
```
sudo wget https://git.kernel.org/pub/scm/utils/dtc/dtc.git/snapshot/dtc-1.4.7.tar.gz 
```
```
sudo tar -xvzf dtc-1.4.7.tar.gz cd dtc-1.4.7/
```
```
sudo make NO_PYTHON=1 PREFIX=/usr/ 
```
```
sudo make install NO_PYTHON=1 PREFIX=/usr/
```
### Installing Vivado HLx 2018.3
Error Occured 

### Installation of Miniterm
Move to the Home folder and run the following command:
```
cd
```
```
sudo apt-get install python-serial
```
### [](https://github.com/ppattanaik/RISC-V_Projects/tree/main/Shakti_On_Artix-7/Installations#installation-of-risc-v-openocd)Installation of RISC-V OpenOCD

Move to the Home folder and run the following commands:

- ***Clone the RISC-V OpenOCD repository***
```
cd
```
```
git clone https://github.com/riscv/riscv-openocd.git
```
```
cd riscv-openocd
```
```
./bootstrap
```
- ***Note:***
```
+ aclocal --warnings=all
+ libtoolize --automake --copy
libtoolize: $pkgltdldir is not a directory: `/mingw/share/libtool'
```
##### ***> If this error is obtained, do not proceed forward. Insted, proceed with ['Setting up the SHAKTI - SDK'](https://github.com/ppattanaik/RISC-V_Projects/tree/main/Shakti_On_Artix-7/Installations#setting-up-the-shakti-sdk) then return to the ['Installation of RISCV - OpenOCD'](https://github.com/ppattanaik/RISC-V_Projects/tree/main/Shakti_On_Artix-7/Installations#installation-of-risc-v-openocd).***

- ***Building the OpenOCD toolchain***
Move to the 'RISCV-OpenOCD' directory and run the following commands:
```
cd riscv-openocd
```
```
export RISCV=/path/to/install/riscv/OpenOCD
```
```
./configure --prefix=$RISCV --enable-remote-bitbang --enable-ftdi--enable-jlink --enable-jtag_vpi --disable-werror
```
```
make
```
```
sudo make install
```
```
export PATH=$PATH:$RISCV/bin
```
Reset or open a new terminal to chack if the installation is successful:
```
reset
```
```
which openocd
```
##### ***>  If the path of OpenOCD is displayed as output, then the RISCV-OpenOCD installation is successful***

### Programming E-arty35t RTL bitstream onto the FPGA 
Pending.

### [](https://github.com/ppattanaik/RISC-V_Projects/tree/main/Shakti_On_Artix-7/Installations#setting-up-the-shakti-sdk)Setting up the SHAKTI-SDK
- ***Pre-requisites***

To solve the software dependencies, move to the home directory and run the following commands:
```
cd
```
```
sudo apt-get install autoconf automake autotools-dev curl make-guile
```
```
sudo apt install libmpc-dev libmpfr-dev libgmp-dev libusb-1.0-0-dev bc
```
```
sudo apt install gawk build-essential bison flex texinfo gperf libtool
```
```
sudo apt install make patchutils zlib1g-dev pkg-config libexpat-dev
```
```
sudo apt install libusb-0.1 libftdi1 libftdi1-2
```
```
sudo apt install libpython3.6-dev
```
- ***Download the SHAKTI-SDK repository***

SHAKTI-SDK repository contains scripts, board support packages to build your application. Move to the home directory and clone it by running the following command :
```
cd
```
```
git clone https://gitlab.com/shaktiproject/software/shakti-sdk.git
```
- ***Download the SHAKTI-TOOLS repository***

The SHAKTI-TOOLS repository contains both 64bit and 32bit toolchain, for building
your application.
Move to the home directory and clone it by running the following command:
```
cd
```
```
git clone --recursive https://gitlab.com/shaktiproject/software/shakti-tools.git
```
- ***Setting up SHAKTI Tool-chain***

From the Home directory, move to Shakti-tools directory and find the tool chain path:
```
cd shakti-tools
```
```
pwd
```
Return to your home diectory and open the .bashrc file:
```
cd
```
```
vi .bashrc
```
To export the tool - chain path copy and paste the syntax below in the .bashrc file and save it:
```
SHAKTITOOLS=/path/to/shakti-tools
export PATH=$PATH:$SHAKTITOOLS/bin:$SHAKTITOOLS/riscv64/bin
export PATH=$PATH::$SHAKTITOOLS/riscv32/bin
export PATH=$PATH:$SHAKTITOOLS/riscv64/riscv64-unknown-elf/bin
export PATH=$PATH:$SHAKTITOOLS/riscv32/riscv32-unknown-elf/bin
```
Replace and add your tool - chain path.
Example:
```
SHAKTITOOLS=/root/shakti-tools
export PATH=$PATH:$SHAKTITOOLS/bin:$SHAKTITOOLS/riscv64/bin
export PATH=$PATH::$SHAKTITOOLS/riscv32/bin
export PATH=$PATH:$SHAKTITOOLS/riscv64/riscv64-unknown-elf/bin
export PATH=$PATH:$SHAKTITOOLS/riscv32/riscv32-unknown-elf/bin
```
- ***Verifying the tool chain Installation***

Open a new terminal and run the following commands:
```
which riscv64-unknown-elf-gcc
```
```
which spike
```
```
which riscv32-unknown-elf-gcc
```
```
which openocd
```
```
which pk
```
##### ***> If the paths of tool chain are displayed as outputs, then the tool chain installation is successful***
