## Building a Virtual Security Home : Splunk Setup & Configuration

![image](https://miro.medium.com/v2/format:webp/1*L7RWj_PxZfuOxpPe3dwrSw.png)

we will set up Splunk (SIEM) in a Ubuntu VM. The VM will be added to the SECURITY subnet. Then we will configure Splunk Universal Forwarder on our Windows Server 2019 (DC) VM which will allow Splunk to ingest logs from the DC.

### Ubuntu Setup
### Downloading the Image
Go to the following URL: [ Download Ubuntu Desktop | Download | Ubuntu|](https://ubuntu.com/download/desktop)
Download the latest LTS version of Ubuntu. As of writing the latest version is **2022.04.3**

The ISO is ~5GB.

![image](https://miro.medium.com/v2/format:webp/1*4wB32QdZofRT2RQ1hRFmNA.png)
After the download is complete you will have a > **.iso** file.

![image](https://miro.medium.com/v2/format:webp/1*eoR6hdcYahUvr5cYe-SU4A.png)

### Creating the VM
In VirtualBox from the sidebar select **Tools** and then click on **New** from the toolbar.

![image](https://miro.medium.com/v2/format:webp/1*SlcAot2I48BFPAkl3ynPuw.png)

Give the VM a name. Select the downloaded ISO image. Select the “Skip Unattended Installation” option and click on **Next.**

![image](https://miro.medium.com/v2/format:webp/1*BgF3O_hR0f4Iap7Lg5CYbQ.png)

Increase the Base Memory to **4096MB (4GB)** and click on **Next**.

![imagge](https://miro.medium.com/v2/format:webp/1*JiIWKTMktN8Mu10-1EIfTw.png)

Increase the Hard Disk size to **100GB** and click on **Next**.

![image](https://miro.medium.com/v2/format:webp/1*0NkkZ-do98gaB-q0AglRGw.png)

Confirm that all the settings look correct and click on **Finish.**

![image](https://miro.medium.com/v2/format:webp/1*Fw5ov7aYpkVcBXcbTwqefg.png)

## Adding VM to Group
Right-click the VM and select “Move to Group” then choose **Home Lab/Security**.

![image](https://miro.medium.com/v2/format:webp/1*0Ve-TCF02XDWMGjrQpEOzw.png)

The final result should look as follows:

![image](https://miro.medium.com/v2/format:webp/1*Chg47hf967wfYd_P2BL8IA.png)

### Configuring the VM

Select the VM and click on Settings from the **toolbar**.

![image](https://miro.medium.com/v2/format:webp/1*pODkaSxcLgZnWWShU71QkQ.png)

Go to **System -> Motherboard**. In Boot Order ensure that **Hard Disk** is on the top followed by **Optical**. Uncheck **Floppy**.

![image](https://miro.medium.com/v2/format:webp/1*fH0Yv2jq0UZO21E0r-HTqQ.png)

Go to **Network -> Adapter 1**. For the Attached to field select **Internal Network**. For name select **LAN 4**. Click on **OK** to save changes.

![image}(https://miro.medium.com/v2/format:webp/1*LvorF9z_U7K46oWW_CMHvw.png)

## Installing Ubuntu
Select the VM and click on **Start**.

![image](https://miro.medium.com/v2/format:webp/1*VSaym0cV21m_yI9KbUpWdg.png)

Press **Enter** to start the Graphical Installer

![image](https://miro.medium.com/v2/format:webp/1*x9IBAyfWkw4n4KH39cQ7WQ.png)

Select your language and click on “Install Ubuntu”.

![image](https://miro.medium.com/v2/format:webp/1*DSuH2Tkd7t2txI_l-vHUMQ.png)

Select Keyboard Layout and click on **Continue.**

![image](https://miro.medium.com/v2/format:webp/1*qzY3XoQ8eXrziQ37s-SQ6A.png)

Enable “Install third-party software for graphics and Wi-Fi hardware and additional media formats” and click on **Continue.**

![image](https://miro.medium.com/v2/format:webp/1*FdGks_ZORjCMSaknSOUAbA.png)

Click on **Install Now**.

![image](https://miro.medium.com/v2/format:webp/1*LPjkoiaWKxT6iekCAWZ74A.png)

Click on **Continue**.

![image](https://miro.medium.com/v2/format:webp/1*VG-fLvznPkCNAXLTz2-8Uw.png)

Select your location and click on **Continue**.

![image](https://miro.medium.com/v2/format:webp/1*pbkw8857w23BtiAQ6I6HEw.png)

Enter the username, password and hostname and click on **Continue**.

![imagge](https://miro.medium.com/v2/format:webp/1*7bQULAEbD_GRsx2biyg2Qw.png)

![image](https://miro.medium.com/v2/format:webp/1*FlkBCn6Ws9A63N3TgBRvDg.png)

Click on **Restart Now** to boot into the system.

![image](https://miro.medium.com/v2/format:webp/1*NNwycZD1XE5Qh0LxiJ2hDg.png)

VirtualBox will automatically remove the ISO file from the disk drive. Press **Enter*** to boot into the newly installed system.

![image](https://miro.medium.com/v2/format:webp/1*M_3CopeHjaWRbCNnEQaLPw.png)

Login using your password.

![image](https://miro.medium.com/v2/format:webp/1*rhwjOmHO1k13VLW3eda-dQ.png)

Complete the post-install setup as shown. Click on **Skip**.

![image](https://miro.medium.com/v2/format:webp/1*RM6yMJk7LpnICkkAJSCv8g.png)

Click on **Next**.

![image](https://miro.medium.com/v2/format:webp/1*j45Bh6n3lVJuVwjZa2Z-iA.png)

Select “No, don’t send system info” and click on **Next**.

![image](https://miro.medium.com/v2/format:webp/1*dtQ-eeAiNU9Yz0CIuEuokg.png)

Ensure this setting is disabled and click on **Next**.

![image](https://miro.medium.com/v2/format:webp/1*3a3f1KQwwY624BQfZUvnpQ.png)

Click on **Done** to close the wizard.

![image](https://miro.medium.com/v2/format:webp/1*r0SNq4TpYIswIo7rRqt4ew.png)

### Post-Install Configuration

### Install Guest Additions
From the VM toolbar select **Devices -> Install Guest Additions CD image**.

![image](https://miro.medium.com/v2/format:webp/1*7naKFgI2SfoVMusA-QV6fQ.png)

The disk will show up on the dock. Click on it to view the content of the disk.

![image](https://miro.medium.com/v2/format:webp/1*ve3oPZzECVOrKvHQzA0tTg.png)

**Right-click** anywhere in the empty area in the File Explorer and select “Open in Terminal”.

![image](https://miro.medium.com/v2/format:webp/1*ltnaEdm5VjJF-sqvMu0e6Q.png)

Run the following command to install Guest Additions:

```bash
sudo ./VBoxLinuxAdditions.run
```

![image](https://miro.medium.com/v2/format:webp/1*e94ozCTRkq2FWmFW57tz-w.png)

Once the installation is complete close the terminal, right-click on the disk icon in the dock and select **Eject**.

![image](https://miro.medium.com/v2/format:webp/1*qfZtLsH5ztjGWMBiQCpElw.png)

### Installing Updates
Press **Ctrl+Alt+T** to open a new terminal then enter the following command to update the system:

```bash
sudo apt update && sudo apt full-upgrade
```

Enter your password when prompted. If there are updates press **Enter** to start the install.

![image](https://miro.medium.com/v2/format:webp/1*EVX3LXPpVyxdNEC_FZ2D8g.png)

## Creating VM Snapshot
Shut down the VM. Click on the Hamburger menu beside the VM name and select **Snapshots**.

![image](https://miro.medium.com/v2/format:webp/1*QjSI3YJiifsohVk6Gs7tlg.png)

Click on **Take** to create a Snapshot.

![image](https://miro.medium.com/v2/format:webp/1*xBV_9VysHM5yYE9yt9b2-w.png)

Provide a descriptive name and click on **OK**.

![image](https://miro.medium.com/v2/format:webp/1*Z9C010xN7jLVcSzbUFAkIQ.png)

Click on the Hamburger menu and click on “Details” to return to the main page.

![image](https://miro.medium.com/v2/format:webp/1*UDMyvCeXIyz6RO0J_BWAoA.png)


## Splunk Installation
### Splunk Download
On the Ubuntu VM go to the following URL: [Splunk Enterprise Free Trial | Splunk](https://www.splunk.com/en_us/download/splunk-enterprise.html). As of writing the latest version of Splunk Enterprise is **9.1.2**.

> To download Splunk you have to create a account.
> Link to get v9.1.2 without an account has been provided at the end of this section.
> If you want to use the latest version follow the steps below to create a account.

Fill in the details in the form, accept the agreement and click on “Create the Account”.

![image](https://miro.medium.com/v2/format:webp/1*jegFTHkfez8YeVmWaXv5fA.png)

After login go to the Linux section and click on the “Download Now” button for the **.deb** file.

![image](https://miro.medium.com/v2/format:webp/1*QlL-y0gsthVO2Re38K3VeA.png)

Scroll down and accept the agreement and then click on “Access program” to start the download.

![imahe](https://miro.medium.com/v2/format:webp/1*IWCb2Ii1aV8-nd7fpRP9XA.png)

Alternatively, use the following link to directly download Splunk v9.1.2:
[Splunk Enterprise 9.1.2 — Linux (.deb) — Direct Download Link](https://download.splunk.com/products/splunk/releases/9.1.2/linux/splunk-9.1.2-b6b9c8185839-linux-2.6-amd64.deb)

## Splunk Installation
Once the download is complete we will have a **.deb** file. Open the Terminal **(Ctrl+Alt+t)** and navigate to the Downloads folder.

````bash
cd Downloads
`````

![image](https://miro.medium.com/v2/format:webp/1*zJ8pfdYmyvVuWMK5EMWJvg.png)

Run the following following command to install curl (dependency for Splunk):

````bash
sudo apt install curl
````

Enter password when prompted.

![image](https://miro.medium.com/v2/format:webp/1*CO_YON_2TcCQTH_tmr6b4g.png)

Run the following command to install Splunk:

````bash
sudo dpkg -i splunk-9.1.2-b6b9c8185839-linux-2.6-amd64.deb
````

Provide a name and password when prompted. These credentials need to be used to log into Splunk.

![iamge](https://miro.medium.com/v2/format:webp/1*VpEyNG6qhcNEGfPOfjuiOQ.png)

Once the setup is complete we see the Splunk is running on **http://127.0.0.1:8000**

![image](https://miro.medium.com/v2/format:webp/1*WV5Ez77hl9RJBOFRmnzhrA.png)

Run the following to allow Splunk to start automatically when the system is booted.

````bash
sudo /opt/splunk/bin/splunk enable boot-start
````

![image](https://miro.medium.com/v2/format:webp/1*VS7mtw-i9-MJAAisiUyfOQ.png)

> You can choose to ignore the last command to enable auto boot.
> If you do not enable run at boot the command that was shown above to start Splunk will need to run to start Splunk

### Creating VM Snapshot
Shut down the VM. Using the Hamburger menu access the Snapshot page. Click on **Take** to create a Snapshot. Give the Snapshot a descriptive name.

![image](https://miro.medium.com/v2/format:webp/1*hsYoq6kcDwNYc3zv3HVapg.png)

![image](https://miro.medium.com/v2/format:webp/1*pE7D5vjTqStOdzxfLSWgnQ.png)

### Splunk Configuration
Before we can install Splunk Universal Forwarder there are a few settings we need to change in Splunk. Open Splunk by going to **http://127.0.0.1:8000.**

![image](https://miro.medium.com/v2/format:webp/1*3Y3USsmcov2y7C5XHr4KeA.png)

From the toolbar select **Settings -> Forwarding and receiving**.

![image](https://miro.medium.com/v2/format:webp/1*O8JPvinUgpRLe8WjDpI1qg.png)

Click on “Add new” in the Receive data section.

![image](https://miro.medium.com/v2/format:webp/1*TJo-cIDLickpo1EZUAO1GA.png)

Enter **9997** as the port to listen for incoming data. Click on **Save**.

![image](https://miro.medium.com/v2/format:webp/1*nZKrpYjFe_-ezaOCey7BDA.png)

![image](https://miro.medium.com/v2/format:webp/1*eDb8fjgKiAxS0QMuiyuzRw.png)

## Universal Forwarder Installation
The next steps need to be performed on the Domain Controller (Windows Server 2019). We are going to ingest the log data that is generated by this device into Splunk

### Universal Forwarder Download
Go to the following link to download Universal Forwarder: [Download Universal Forwarder for Remote Data Collection | Splunk](https://www.splunk.com/en_us/download/universal-forwarder.html)

You need to log in to be able to download the setup. Select the Windows tab and then click on the Download Now button beside the 64-bit option.

![image](https://miro.medium.com/v2/format:webp/1*_ULXa5qzY8e0wNAfidX3_A.png)

Alternatively, Splunk Universal Forwarder v9.1.2 can be downloaded directly using the following link: [Splunk Universal Forwarder 9.1.2 — Windows (.msi) — Direct Download Link](https://download.splunk.com/products/universalforwarder/releases/9.1.2/windows/splunkforwarder-9.1.2-b6b9c8185839-x64-release.msi)

## Universal Forwarder Install
Double-click on the **.msi** file to begin installation.

![image](https://miro.medium.com/v2/format:webp/1*PFD0tBrpW0PyB8UjSFkvlg.png)

Check the box on the top to accept the agreement and then click on **Next**.

![image](https://miro.medium.com/v2/format:webp/1*SctsCNNKrN_KO05X4JPtiQ.png)

Provide a username and password for the Forwarder. I would recommend using the same credentials that were configured on Splunk.

![image](https://miro.medium.com/v2/format:webp/1*BvgBHF_8wnam9rbh_6S1Yg.png)

For the new step need the IP address of the Ubuntu (Splunk) VM. Use the following command to get the IP address.

````bash
ip addr
````

Use the IP address that is shown under **enp0s3**.

> If in your case instead of **enp0s3** you see eth0 use the IP address that is shown under that section.

![image](https://miro.medium.com/v2/format:webp/1*wIZtZ0l5pB68ggYOE2DpHw.png)

Enter the IP address of the Splunk VM (in my case **10.10.10.13**) and enter **8089** as the value for the port field then click on **Next**.

![image](https://miro.medium.com/v2/format:webp/1*sbPJTVacDy_qnkE461BOiw.png)

Again enter the Splunk VM IP address and for port enter **9997**. This is the port we configured in Splunk. Click on **Next** to continue.

![image](https://miro.medium.com/v2/format:webp/1*uQxvfAfvwm82yFeX-6-lIw.png)

Click on **Install**

Click on Finish to close the installer.

![image](https://miro.medium.com/v2/format:webp/1*YHIAOnmyJd0d0NELD53SFw.png)

## Data Ingestion Configuration
Now that we have Splunk and Universal Forwarder configured we need to link both the pieces together so that Splunk can collect data.

### Adding Data Source
In Splunk select **Settings -> Add Data**.

![image](https://miro.medium.com/v2/format:webp/1*70Epwvi8aaGTCHemoF13BQ.png)

Click on **Forward**.

![image](https://miro.medium.com/v2/format:webp/1*CD5CDQrZD55w933Irntm0w.png)

Our DC VM should automatically show up in the left box. Click on “add all” to move it to the right side. In the “New Source Class Name” field provide a name for the source. Click on **Next** to continue.

![image](https://miro.medium.com/v2/format:webp/1*pGlG4ctBjI78pRvKDYOKFg.png)

Select “Local Event Logs” then click on the “add all” button above the dropdown field to ingest all the logs generated by the DC. Click on **Next** once done.

![image](https://miro.medium.com/v2/format:webp/1*7ERtwIdaesX4nIV4C5ZX0Q.png)

Click on “Create a new index”.Indexes are the Splunk equivalent of SQL Tables. It is used to store similar data.

![image](https://miro.medium.com/v2/format:webp/1*DPUUecvmXUyfvctSqFLqLw.png)

Provide the Index a name. Keep all the other fields on their default value and click on **Save*** then click on **Next**.

![image](https://miro.medium.com/v2/format:webp/1*lcIgKOV8sPTZvUcBKAq28g.png)

Confirm all the options look correct and click on **Submit**.

![image](https://miro.medium.com/v2/format:webp/1*0TzYhOaLyd5QUHgTA6u4jg.png)

### Querying Data
From the Splunk toolbar select **Apps -> Search & Reporting**.

![image](https://miro.medium.com/v2/format:webp/1*uuPns5rf0R6WEjhs9mmbmA.png)

In the search box enter the following to view the ingested data:

````bash
index="windows"
````

![image](https://miro.medium.com/v2/format:webp/1*uH0E2huzBqBT1xGMgYnCaw.png)

> If the search does not return any value, wait for 2–3 minutes and then try again. If there is still no data go to the Windows VM and perform some simple actions (open applications, change settings, etc.) then after sometime you should see data flowing into > Splunk.



