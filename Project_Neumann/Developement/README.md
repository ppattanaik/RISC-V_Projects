
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
	
	
	
	
## Troubleshooting
