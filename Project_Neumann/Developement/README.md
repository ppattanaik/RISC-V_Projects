
# Project_Neumann

## The PULP Platform :
PULPino is an open-source single-core microcontroller system, based on 32-bit RISC-V cores
developed at ETH Zurich. PULPino is configured to use either the RISCY or the zero-riscy core.
RISCY is an in-order, single-issue core with 4 pipeline stages whereas zero-riscy core with 2 stage
pipeline.

 - #### ***Setting up the PULP Platform :***
	 -  Download and install [Ubuntu 20.04 LTS](https://ubuntu.com/download/desktop/thank-you?version=20.04.2.0&architecture=amd64)
	 -  Open terminal and execute the following commands:
	 
	```sudo apt-get update```
	
	```sudo apt-get upgrade```
	
	```sudo apt-get install tcsh``` // for tcl scripts
	
	```sudo apt-get install cmake``` // for cmake script
	
	```sudo apt-get install git``` // for cmake script
	
	```sudo apt-get install vim-gtk3``` // for gvim (ignore if gvim is already installed)
	
	 - Move to Desktop and make your work directory
		- Example :
		
		``` cd Desktop```
		
		``` mkdir project_neumann```
		
	- Make a RISCV environment in your local PC
	
	```cd project_neumann```
	
	```mkdir RISC-V``` // create a RISC-V named folder in your work directory
	
	```mkdir pulptoolchain``` // for storing the pulpino cross compiler
	
	- Move to the RISC-V directory and clone the pulp-riscv-gnu-toolchain in it
	
	```cd RISC-V```
	
	```git clone --recursive https://github.com/pulp-platform/pulp-riscv-gnu-toolchain```
	
	- Set the PATH variable in the environment file and add the pulpinotoolchain/bin path to it.
	
	```sudo gvim /etc/environment``` // it will opens the environment file to change the PATH variable
	
	- Add the below mentioned path in the file
		``` 
		PATH="/home/vlsi_lab/Desktop/project_neumann/pulptoolchain/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin"
		```
	- Log out from the system and re-login so that the $PATH changes system wide.
	- Install below software packages:
		```
		sudo apt-get install autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev
		```
	- Now, go to the pulp-riscv-gnu-toolchain directory and execute below command, it may take 1.5 hours to build the entire pulp-riscv-gnu-toolchain :
	
	```cd pulp-riscv-gnu-toolchain```
		
	```
	./configure --prefix=/home/vlsi_lab/Desktop/project_neumann/pulptoolchain --with-arch=rv32imc --with-cmodel=medlow --enable-multilib
	```
		
	```make clean```
		 
	```sudo make``` // installation starts from here
	
	- Ensure the ​ riscv32-unknown-elf-gcc ​ and other riscv32-unknown binaries are created in the ​ /home/username/Desktop/pulptoolchain/bin ​ folder.
	- Further ensure that the command below should give its path in the terminal.
	
	``` which riscv32-unknown-elf-gcc``` ​ 
	
	##### ***> If the above command do not give any output in the terminal then provide its path in the .bashrc as well as the environment file and re-execute the command***
	
	- Now, move to RISC-V folder and clone the ​ pulpino platform​ git db by executing below command
	
	```git clone ​https://github.com/pulp-platform/pulpino```
	
	##### ***> Copying the above command may cause the following error***
	
	```fatal: protocol '​https' is not supported```
	
	##### ***//Manually type the command to avoid this error***
	
	- Ensure that python2 is the default python or python2 is the only python in your PC.
	- To install python 2 execute the following command:
	
	```sudo apt install python```
	
	- Check the version by typing the following command:
	
	```python --version```
	
	- Install pip by executing the following command in the terminal;
		##### ***(As Pip for Python 2 is not included in the Ubuntu 20.04 repositories. We’ll be installing pip for Python 2 using the `get-pip.py` script.)***
		- Start by enabling the universe repository:
		
		```sudo add-apt-repository universe```
		
		- Update the packages index and install Python 2:
		
		```sudo apt update```
		
		```sudo apt install python2``` (Ignore this step if Python2 is already installed)
		
		- Use [`curl`](https://linuxize.com/post/curl-command-examples/) to download the `get-pip.py` script:
		
		```curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py```
		
		- Once the repository is enabled, run the script as sudo user with `python2` to install pip for Python 2:
		
		```sudo python2 get-pip.py```
		
		- Check whether pip is successfully installed or not
		
		```pip --version ```
		
		```
		Output
		pip 20.0.2 from /usr/local/lib/python2.7/dist-packages/pip (python 2.7)
		```
		
	- Install yaml program by using ​ the following command:
	
	```pip install pyyaml​``` (Copying the following command may cause error. To 	avoid it manually type this command)
	
	- Go to ​ pulpino​ directory and run the update-ips.py using the​ command:
	
	```./​update-ips.py```
	
	//this should successfully run without any error and various IP databases should be in the current directory
	
	- Go to ​ sw​ folder and create a folder named build
	
	```mkdir build```
	
	- Move to the build directory and copy the cmake_configure.zeroriscy.gcc.sh​ script file from ​ sw​ folder to it
	
	```cd ​ build​```
	
	```cp ​ ../cmake_configure.zeroriscy.gcc.sh .```
	
	- Edit the above cmake script file and save it:
	
	``` vim cmake_configure.zeroriscy.gcc.sh```
	
		- Find and remove the ​ -m32​ flag (Probably present in the 13th line)
		- Make ​ZERO_RV32M=0 (Probably present in the 26th line)
		- Modify ​RV32IM​ to ​ rv32IM (Probably present in the 31st line)
		- Save the file
	
	- Open the ​ CMakeLists.txt​ file in the ​ sw​ folder and remove the ​ -m32​ flag in the 54th line or wherever you find it.
	
	-  Go to the ​ build​ folder and execute the cmake script

```./​cmake_configure_riscv.gcc.sh​``` (Errors may pop up)

	- Copy the ​ riscv.ld​ file from pulp-gnu-toolchain to build/CMakeFiles/CMakeTmp directory.
	- Execute this command:

	```
	riscv32-unknown-elf-ld --verbose | head -n -1 | tail -n +7 | sed '168 a \ \_fbss = .;' | sed '169 a \ \ . = .;' > /home/vlsi_lab/Desktop/project_neumann/RISC-V/pulpino/sw/build/CMakeFiles/CMakeTmp/riscv.ld
	```
	- Run cmake script file ​ cmake_configure_riscv.gcc.sh​ ​ again by using

	```./​cmake_configure_riscv.gcc.sh```
	
	- Repeat the previous 3 commands again.
	
	- It should run successfully and gives you below output:
	
	```
	vlsi_lab@vlsi-lab:~/Desktop/project_neumann/RISC-V/pulpino/sw/build$./cmake_configure.zeroriscy.gcc.sh 
	System is unknown to cmake, create:
	Platform/Linux-CXX to use this system, please post your config file on discourse.cmake.org so it can be added to cmake
	Your CMakeCache.txt file was copied to CopyOfCMakeCache.txt. Please post that file on discourse.cmake.org.
	-- GCC_MARCH= rv32IM
	-- USE_ZERO_RISCY= 1
	-- RISCY_RV32F= 0
	-- ZERO_RV32M= 0
	-- ZERO_RV32E= 0
	-- PL_NETLIST= 
	-- Configuring done
	-- Generating done
	-- Build files have been written to: /home/vlsi_lab/Desktop/project_neumann/RISC-V/pulpino/sw/build
	```
	
	
	
## Troubleshooting
