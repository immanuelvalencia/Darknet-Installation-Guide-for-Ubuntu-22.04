# CUDA 11.7 and cuDNN 8.4.0 for Ubuntu 22.04

## Initial setup
*For fresh Ubuntu 22.04 Installation*

**Update your OS**

	sudo apt update
	sudo apt upgrade
	sudo reboot

**Fix System Time**
*For Windows and Ubuntu dual boot*

    timedatectl set-local-rtc 1



## CUDA Toolkit 11.7 Installation
1. **Run the following codes in the terminal** (***CTRL + Alt + T***).
	```
	wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
	```
	```
	sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
	```
	```
	wget https://developer.download.nvidia.com/compute/cuda/11.7.1/local_installers/cuda-repo-ubuntu2204-11-7-local_11.7.1-515.65.01-1_amd64.deb
	```
	```
	sudo dpkg -i cuda-repo-ubuntu2204-11-7-local_11.7.1-515.65.01-1_amd64.deb
	```
	```
	sudo cp /var/cuda-repo-ubuntu2204-11-7-local/cuda-*-keyring.gpg /usr/share/keyrings/
	```
	```
	sudo apt-get update
	```
	```
	sudo apt-get -y install cuda
	```

2. **Open your profile settings via terminal**
``` gedit ~/.profile```

	then the following lines at the end

	    #CUDA Path
	    export PATH=/usr/local/cuda-11.7/bin${PATH:+:${PATH}}

3. **Save then restart your device.**
		
		sudo reboot

4. **Test CUDA Installation**

		nvidia-smi
		nvcc --version

> 		If successful, it will output the following:

		+-----------------------------------------------------------------------------+
		| NVIDIA-SMI 515.65.01    Driver Version: 515.65.01    CUDA Version: 11.7     |
		|-------------------------------+----------------------+----------------------+
		| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
		| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
		|                               |                      |               MIG M. |
		|===============================+======================+======================|
		|   0  NVIDIA GeForce ...  On   | 00000000:0A:00.0  On |                  N/A |
		|  0%   52C    P8    43W / 350W |    388MiB / 12288MiB |      1%      Default |
		|                               |                      |                  N/A |
		+-------------------------------+----------------------+----------------------+
		                                                                               
		+-----------------------------------------------------------------------------+
		| Processes:                                                                  |
		|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
		|        ID   ID                                                   Usage      |
		|=============================================================================|
		|    0   N/A  N/A      1995      G   /usr/lib/xorg/Xorg                202MiB |
		|    0   N/A  N/A      2355      G   /usr/bin/gnome-shell               29MiB |
		|    0   N/A  N/A      3109      G   ...944559455204059567,131072      122MiB |
		|    0   N/A  N/A      4142      G   ...AAAAAAAAA= --shared-files       30MiB |
		+-----------------------------------------------------------------------------+


> nvcc output


    nvcc: NVIDIA (R) Cuda compiler driver
    Copyright (c) 2005-2022 NVIDIA Corporation
    Built on Wed_Jun__8_16:49:14_PDT_2022
    Cuda compilation tools, release 11.7, V11.7.99
    Build cuda_11.7.r11.7/compiler.31442593_0


## cuDNN 8.4.0.27 Installation
The process here are taken from the official documentation
https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html#install-linux
1. **Download cuDNN v8.4.0 for CUDA 11.x**
https://developer.nvidia.com/rdp/cudnn-archive
	Local Installer for Ubuntu20.04 x86_64 (Deb)

2. Open your terminal and navigate to your Downloads folder or where you saved the deb file.

	    cd Downloads
	    
 3. Run the following codes
	
	**3.1 Enable the local repository**
	 ``` sudo dpkg -i cudnn-local-repo-ubuntu2004-8.4.0.27_1.0-1_amd64.deb```
	 
	 **3.2 Import the CUDA GPG key.**
	```sudo apt-key add /var/cudnn-local-repo-ubuntu2004-8.4.0.27/7fa2af80.pub```

	**3.3 Refresh the repository metadata.**
	```sudo apt-get update```
	
	**3.4 Install the runtime, developer libraries and code samples**
	```sudo apt-get install libcudnn8=8.4.0.27-1+cuda11.6```
	```sudo apt-get install libcudnn8-dev=8.4.0.27-1+cuda11.6```
	```sudo apt-get install libcudnn8-samples=8.4.0.27-1+cuda11.6```
	```sudo apt-get install libfreeimage3 libfreeimage-dev```
	**3.5 Verifying the install**
	```cp -r /usr/src/cudnn_samples_v8/ $HOME```
	```cd  $HOME/cudnn_samples_v8/mnistCUDNN```
	```make clean && make```
	```./mnistCUDNN```


	If cuDNN is properly installed and running on your Linux system, you will see a message similar to the following:
	> Test passed!
