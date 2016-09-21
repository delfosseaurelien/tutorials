---
layout: tutorial
title: Tutorial 0 Download, Install and Start NiFi
tutorial-id: 640
tutorial-series: Basic Development
tutorial-version: hdf-2.0.0
intro-page: false
components: [ nifi ]
---

# Tutorial 0: Download, Install, and Start NiFi

## Introduction

In this tutorial, you learn about the NiFi environment, how to install NiFi onto Hortonworks Sandbox or on a local machine, and how to start NiFi.

## Pre-Requisites
- Completed Learning the Ropes of Apache NiFi-Introduction.
- Downloaded and installed [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/). (Required for Step 2, Option 1 for NiFi installation.)
- For Windows users, download [Git Bash](https://openhatch.org/missions/windows-setup/install-git-bash) to run Linux terminal commands in these tutorials.
- If on mac or linux, added `sandbox.hortonworks.com` to your `/private/etc/hosts` file
- If on windows 7, added `sandbox.hortonworks.com` to your `/c/Windows/System32/Drivers/etc/hosts` file

The following terminal commands in the tutorial instructions are performed in VirtualBox Sandbox and Mac machine. For windows users, to run the following terminal commands, download [Git Bash](https://openhatch.org/missions/windows-setup/install-git-bash).

If on mac or linux, to add `sandbox.hortonworks.com` to your list of hosts, open the terminal, enter the following command, replace {Host-Name} with the appropriate host for your sandbox:

~~~bash
echo '{Host-Name} sandbox.hortonworks.com' | sudo tee -a /private/etc/hosts
~~~

If on windows 7, to add `sandbox.hortonworks.com` to your list of hosts, open git bash, enter the following command, replace {Host-Name} with the appropriate host for your sandbox:

~~~bash
echo '{Host-Name} sandbox.hortonworks.com' | tee -a /c/Windows/System32/Drivers/etc/hosts
~~~

![changing-hosts-file.png](/assets/realtime-event-processing-with-hdf/lab0-nifi/changing-hosts-file.png)

## Outline
- [Step 1: Explore NiFi Environment Before NiFi Installation](#explore-nifi-environment)
  - [1.1 Plan to Install HDF 2.0 on Sandbox](#install-hdf-on-sandbox)
  - [1.2 Plan to Install HDF 2.0 on Local Machine](#install-hdf-on-machine)
- [Step 2: Download and Install NiFi on Sandbox (Option 1)](#download-nifi-sandbox)
- [Step 3: Download and Install NiFi on Local Machine (Option 2)](#download-nifi-machine)
- [Step 4: Start NiFi on Sandbox](#start-nifi-sandbox)
  - [4.1 Forward Port with VirtualBox GUI](#forward-port-virtualbox)
  - [4.2 Forward Port with Azure GUI](#forward-port-azure)
- [Step 5: Start NiFi on Local Machine](#start-nifi-locally)
- [Summary](#summary-lab0)

### Step 1: Explore NiFi Environment Before NiFi Installation <a id="explore-nifi-environment"></a>

You can run NiFi inside a single virtual machine or on your local computer. This version of the tutorial instructions are based on [Hortonworks DataFlow 2.0 GZipped](http://hortonworks.com/downloads/). There are 2 ways to download and install HDF 2.0: Option 1 on a Hortonworks Sandbox 2.5 Virtual Image or Option 2 on your local machine. HDF comes in 2 versions with only NiFi or with NiFi, Kafka, Storm, and Zookeeper. For this tutorial series, you should download HDF with NiFi only. The necessary components are:
- HDF 2.0 (NiFi only)
- Internet Access

### 1.1 Plan to Install HDF 2.0 on Sandbox <a id="install-hdf-on-sandbox"></a>

If you plan to install HDF on Hortonworks Sandbox, review the table, and proceed to step 2.

**Table 1: Hortonworks Sandbox VM Information**

| Parameter  | Value (VirtualBox)  | Value(VMware)  | Value(MS Azure)  |
|:---|:---:|:---:|---:|
| Host Name  | 127.0.0.1  | 172.16.110.129  | 23.99.9.233  |
| Port  | 2222  | 2222  | 22  |
| Terminal Username  | root  | root  | {username-of-azure}  |
| Terminal Password  | hadoop  | hadoop  | {password-of-azure}  |


> Note: **Host Name** values are unique for VMware & Azure Sandbox compared to the table. For VMware and VirtualBox, **Host Name** is located on the Welcome screen. For Azure, **Host Name** is located under **Public IP Address** on the Sandbox Dashboard. For Azure users, you created the terminal **username** and **password** while deploying the Sandbox on Azure. For VMware and VirtualBox users, you change the terminal password after first login.

If it is your first time using the Sandbox VM, you might be prompted to change the default 'hadoop' password. Run the following command and provide a stronger password:

~~~
ssh -p 2222 root@localhost
root@localhost's password:
You are required to change your password immediately (root enforced)
Last login: Wed Jun 15 19:47:44 2016 from 10.0.2.2
Changing password for root.
(current) UNIX password:
New password:
Retype new password:
[root@sandbox ~]#
~~~

### 1.2 Plan to Install HDF 2.0 on Local Machine <a id="install-hdf-on-machine"></a>

You should read this section if you plan to install NiFi on your local machine. Once you have verified that your machine meets system requirements, proceed to Step 3.

Does your system meet HDF's installation requirements?

Supported OS for HDF Installation:
- Linux Red Hat/Cent OS 6 or 7) 64-bit
- Ubuntu 12.04 or 14.04 64-bit
- Debian 6 or 7
- SUSE Enterprise 11-SP3
- MAC OS X
- Windows OS

Supported Browsers:
- Mozilla Firefox latest
- Google Chrome latest
- MS Edge
- Safari 8

Supported JDKS:
- Open JDK7 or JDK8
- Oracle JDK 7 or JDK 8

Supported HDP Versions that Interoperate with HDF:
- HDP 2.3.x
- HDP 2.4.x
- HDP 2.5.x

Two Versions of HDF

Version 1 only comes with NiFi.
- On the Hortonworks HDF downloads page, version 1 is available.

Version 2 comes with NiFi, Kafka, Storm and Zookeeper
- This version is available in Hortonworks Documentation

### Step 2: Download and Install NiFi on Hortonworks Sandbox (Option 1) <a id="download-nifi-sandbox"></a>
This tutorial uses Hortonworks Sandbox 2.5.

HDF is installed on the Hortonworks Sandbox VirtualBox image because the Sandbox does not come with HDF preinstalled.

Use the following steps to guide you through the NiFi installation:

1\. Open a terminal window (Mac and Linux) or git bash (Windows) on **sandbox**.

~~~
ssh root@127.0.0.1 -p 2222
~~~

2\. Download the **jdkinstall_nifi.sh** file from the github repo. Copy & paste the following commands:

~~~
cd
wget https://raw.githubusercontent.com/hortonworks/tutorials/hdp/assets/learning-ropes-nifi-lab-series/automation-scripts/jdkinstall_nifi.sh
chmod +x ./jdkinstall_nifi.sh
~~~

3\. Let's navigate back to our local machine. Open a browser. Download NiFi from [HDF Downloads Page](http://hortonworks.com/downloads/). There are two package options: one for HDF TAR.GZ file tailored to Linux and ZIP file more compatible with Windows. Mac can use either option. For the tutorial,  download the latest HDF TAR.GZ:

![download_hdf_iot](/assets/learning-ropes-nifi-lab-series/lab0-download-install-start-nifi/download-hdf-learn-ropes-nifi.png)

4\. Now we need to send NiFi from our local machine to the sandbox virtual machine.
Open a terminal for your local machine. If your HDF program was downloaded to the
**Downloads** folder, navigate to it. `cd ~/Downloads`, then we can perform
the transport.

~~~
scp -P 2222 HDF-2.0.0.0-579.tar.gz root@127.0.0.1:/root
~~~

> Note: For VMware and Azure users, the sandbox IP address may be different, so replace 127.0.0.1 with your appropriate IP. Use the ssh-port provided in Table 1. hdf-version is the digits in the tar.gz name you downloaded, for example the numbers in bold HDF-**2.0.0.0-579**.tar.gz. If your HDF version number is different, replace the number in the example with the number you have.

5\. Now the nifi install script we downloaded earlier, comes back. Run the script from your sandbox terminal:

~~~
./jdkinstall_nifi.sh
~~~

### Step 3: Download and Install NiFi on Local Machine (Option 2) <a id="download-nifi-machine"></a>

1\. Open a browser. Download NiFi from [HDF Downloads Page](http://hortonworks.com/downloads/). You will see two HDF download links, both include HDF that only comes with NiFi packaged. There are two package options: one for HDF TAR.GZ file tailored to Linux and zip file more compatible with Windows. Mac can use either option. In this tutorial section, download the zip on a Mac:

![download_hdf_iot](/assets/learning-ropes-nifi-lab-series/lab0-download-install-start-nifi/download-hdf-learn-ropes-nifi.png)

2\. After downloading NiFi, it will be in a compressed format. To install NiFi, extract the files from the compressed file to a location in which you want to run the application. For the tutorial, we moved the extracted HDF folder to the `Applications` folder.

The image below shares NiFi downloaded and installed in the Applications folder:

![download_install_nifi](/assets/learning-ropes-nifi-lab-series/lab0-download-install-start-nifi/download_install_nifi.png)

### Step 4: Start NiFi on Sandbox <a id="start-nifi-sandbox"></a>

Use the following steps to start NiFi if you downloaded and installed it on Hortonworks Sandbox. For information about how to start NiFi on your local machine, go to step 5.

In this tutorial, launch NiFi in the background.

1\. Open a terminal (Mac and Linux) or git bash (Windows). SSH into the Hortonworks Sandbox:

~~~
ssh root@127.0.0.1 -p 2222
~~~

2\. Navigate to the `bin` directory using the following command:

~~~
cd hdf/HDF-2.0.0.0/nifi/bin
~~~

3\. Run the `nifi.sh` script to start NiFi:

~~~
./nifi.sh start
~~~

> Note: To stop NiFi, type `./nifi.sh stop`

Open the NiFi DataFlow at `http://sandbox.hortonworks.com:9090/nifi/` to verify NiFi started. Wait 1 minute for NiFi to load. If NiFi HTML interface does not load, verify the value in the nifi.properties file matches **nifi.web.http.port=9090**.

4\. Navigate to the **conf** folder and open nifi.properties in the vi editor.

~~~
cd ../conf
vi nifi.properties
~~~

5\. Type `/nifi.web.http.port` and press enter. Verify `9090` is the value of nifi.web.http.port as below, else change it to this value:

~~~
nifi.web.http.port=9090
~~~

To exit the vi editor, press `esc` and then enter `:wq` to save the file.
Now that the configuration in the nifi.properties file is updated, port forward a new NiFi port because the VM is not listening for the port **9090**, so NiFi does not load on the browser. If you are using VirtualBox Sandbox, refer to section 4.1. For Azure Sandbox users, refer to section 4.2.

### 4.1 Forward Port with VirtualBox GUI <a id="forward-port-virtualbox"></a>

1\. Open VirtualBox Manager

2\. Right-click your running Hortonworks Sandbox, and select **settings**.

3\. Go to the **Network** Tab

Click the button that says **Port Forwarding**. Overwrite NiFi entry with the following values:

| Name  | Protocol  | Host IP  | Host Port  | Guest IP  | Guest Port  |
|:---|:---:|:---:|:---:|:---:|---:|
| NiFi  | TCP  | 127.0.0.1  | 9090  |   | 9090  |

![port_forward_nifi_iot](/assets/learning-ropes-nifi-lab-series/lab0-download-install-start-nifi/port_forward_nifi_iot.png)


4\. Open NiFi at `http://sandbox.hortonworks.com:9090/nifi/`. Wait 1 to 2 minutes for NiFi to load.

> Note: If you have not configured the `sandbox.hortonworks.com` alias in `/etc/hosts`, try the `http://localhost:9090/nifi` URL as well.

### 4.2 Forward Port with Azure GUI <a id="forward-port-azure"></a>

1\. Open Azure Sandbox.

2\. Click the Sandbox with the **shield icon**.

![shield-icon-security-inbound.png](/assets/learning-ropes-nifi-lab-series/lab0-download-install-start-nifi/shield-icon-security-inbound.png)

3\. Under **Settings**, in the **General** section, click **Inbound Security Rules**.

![inbound-security-rule.png](/assets/learning-ropes-nifi-lab-series/lab0-download-install-start-nifi/inbound-security-rule.png)

4\. Scroll to **NiFi**, and click on the row.

![list-nifi-port.png](/assets/learning-ropes-nifi-lab-series/lab0-download-install-start-nifi/list-nifi-port.png)

5\. Verify the **Destination Port Range** value is 9090, else change it to that.

![change-nifi-port.png](/assets/learning-ropes-nifi-lab-series/lab0-download-install-start-nifi/change-nifi-port.png)

6\. Open NiFi at `http://sandbox.hortonworks.com:9090/nifi/`. Wait 1 to 2 minutes for NiFi to load.


### Step 5: Start NiFi on Local Machine <a id="start-nifi-locally"></a>

If you downloaded and installed NiFi on your local machine, use this step to start NiFi.

There are 3 methods to start NiFi: launch NiFi in foreground, in the background or as a service. See the [Starting NiFi Section](http://docs.hortonworks.com/HDPDocuments/HDF2/HDF-2.0.0/bk_command-line-installation/content/starting-nifi.html) in the HDF Documentation to learn more.

1\. To start NiFi in the background, open a terminal window or git bash, navigate to NiFi installation directory, and enter:

~~~bash
./HDF-2.0.0.0/nifi/bin/nifi.sh start
~~~

2\. Open NiFi at `http://sandbox.hortonworks.com:8080/nifi/`. Wait 1 to 2 minutes for NiFi to load.

## Summary <a id="summary-lab0"></a>

Congratulations! You learned that NiFi can be installed on a VM or directly on your computer. You also learned to download, install, and start NiFi. Now that you have NiFi is up and running, you are ready to build a dataflow.

## Further Reading
For more information on NiFi Configuration, see the [System Administrator's Guide](http://docs.hortonworks.com/HDPDocuments/HDF1/HDF-1.2.0.1/bk_AdminGuide/content/index.html).