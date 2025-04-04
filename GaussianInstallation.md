---


---

<h1 id="gaussian-splatting-nerfstudio-installation-guide">Gaussian Splatting Nerfstudio Installation Guide</h1>
<p>Before starting the installation of <strong>Gaussian Splatting Nerfstudio</strong>, ensure you have <strong>Ubuntu 24.04</strong> installed. If you don’t have any version of Ubuntu on your system, you can skip to section <strong>B</strong> to install <strong>Ubuntu 24.04</strong> and if you already have <strong>Ubuntu 24.04</strong> installed, skip ahead to <strong>Section C</strong> where the installation of <strong>Gaussian Splatting Nerfstudio</strong> begins.</p>
<hr>
<h2 id="a.-uninstalling-older-versions-of-ubuntu">A. Uninstalling Older Versions of Ubuntu</h2>
<p>If you have an older version of Ubuntu installed and need to upgrade to Ubuntu 24.04, you must first remove the existing installation. This section will guide you through the process of uninstalling Ubuntu safely before proceeding with the installation of the new version.</p>
<h3 id="step-1-access-disk-management-in-windows">Step 1: Access Disk Management in Windows</h3>
<p>Before uninstalling Ubuntu, you need to access Windows and open Disk Management to locate the partitions used by Ubuntu.</p>
<ol>
<li>Boot into Windows.</li>
<li>Open Disk Management by right-clicking the Windows icon and selecting <strong>Disk Management</strong>.</li>
</ol>
<h3 id="step-2-delete-ubuntu-partitions">Step 2: Delete Ubuntu Partitions</h3>
<p>Once in Disk Management, locate the partitions used by Ubuntu and delete them.</p>
<ol>
<li>Identify the partitions labeled as <strong>Ext4</strong>, <strong>Linux Swap</strong>, or <strong>EFI System Partition</strong> (if used by Ubuntu).</li>
<li>Right-click on each Ubuntu-related partition and select <strong>Delete Volume</strong>.</li>
<li>Confirm the deletion when prompted.</li>
</ol>
<h3 id="step-3-extend-windows-partition">Step 3: Extend Windows Partition</h3>
<p>After deleting the Ubuntu partitions, the freed space needs to be allocated back to Windows.</p>
<ol>
<li>Right-click on the main Windows partition (usually <strong>C:</strong>).</li>
<li>Select <strong>Extend Volume</strong>.</li>
<li>Follow the on-screen instructions to merge the unallocated space with the Windows partition.</li>
</ol>
<h3 id="step-4-assign-a-drive-letter-to-the-efi-partition">Step 4: Assign a Drive Letter to the EFI Partition</h3>
<p>To ensure that the system is properly cleaned up, we need to assign a drive letter to the EFI partition using the Command Prompt.</p>
<ol>
<li>Open <strong>Command Prompt</strong> as Administrator:
<ul>
<li>Search for <strong>cmd</strong> in the Windows search bar.</li>
<li>Select <strong>Run as administrator</strong>.</li>
</ul>
</li>
<li>Type the following command to open the Disk Partitioning tool:<pre class=" language-sh"><code class="prism  language-sh">diskpart
</code></pre>
This will enter the Disk Partition utility, and you should see a message indicating that <code>DISKPART</code> is running.</li>
<li>List the available disks:<pre class=" language-sh"><code class="prism  language-sh">list disk
</code></pre>
This will display all the disks connected to the system. Identify the disk where Ubuntu was installed (usually <strong>Disk 0</strong>).</li>
<li>Select the appropriate disk:<pre class=" language-sh"><code class="prism  language-sh">select disk 0
</code></pre>
If your Ubuntu installation was on a different disk, replace <code>0</code> with the correct disk number.</li>
<li>List the partitions on the selected disk:<pre class=" language-sh"><code class="prism  language-sh">list partition
</code></pre>
This will display all partitions on the disk. Locate the <strong>EFI System Partition</strong>, usually <strong>Partition 1</strong>.</li>
<li>Select the EFI partition:<pre class=" language-sh"><code class="prism  language-sh">select partition 1
</code></pre>
If the EFI partition is a different number, replace <code>1</code> with the correct partition number.</li>
<li>Assign a drive letter (e.g., <code>z:</code>) to the partition to make it accessible:<pre class=" language-sh"><code class="prism  language-sh">assign letter=z
</code></pre>
</li>
<li>Exit <code>diskpart</code>:<pre class=" language-sh"><code class="prism  language-sh">exit
</code></pre>
Now, the EFI partition should be accessible under <strong>z:</strong> in File Explorer.</li>
</ol>
<h3 id="step-5-remove-ubuntu-from-efi-partition">Step 5: Remove Ubuntu from EFI Partition</h3>
<p>Now that the EFI partition is accessible, follow these steps to delete Ubuntu’s boot entry:</p>
<ol>
<li>In the Command Prompt, switch to the EFI partition:<pre class=" language-sh"><code class="prism  language-sh">z:
</code></pre>
</li>
<li>Navigate to the EFI folder:<pre class=" language-sh"><code class="prism  language-sh">cd EFI
</code></pre>
</li>
<li>List the contents of the EFI directory:<pre class=" language-sh"><code class="prism  language-sh">dir
</code></pre>
You should see folders like <code>Boot</code>, <code>Microsoft</code>, and <code>Ubuntu</code>.</li>
<li>Remove the Ubuntu boot entry:<pre class=" language-sh"><code class="prism  language-sh">rd /s Ubuntu
</code></pre>
When prompted, type <code>Y</code> and press <strong>Enter</strong> to confirm.</li>
<li>Verify the removal:<pre class=" language-sh"><code class="prism  language-sh">dir
</code></pre>
The <code>Ubuntu</code> folder should no longer be listed.</li>
</ol>
<p>At this point, Ubuntu has been completely removed from your system, and you can proceed with installing Ubuntu 24.04.</p>
<h2 id="b.-installing-ubuntu-24.04-lts">B. Installing Ubuntu 24.04 LTS</h2>
<p>If you don’t have Ubuntu installed on your system, follow these steps to install <strong>Ubuntu 24.04 LTS</strong>.</p>
<h3 id="step-1-download-ubuntu-24.04-lts">Step 1: Download Ubuntu 24.04 LTS</h3>
<p>Before installing Ubuntu, you need to download the latest <strong>Ubuntu 24.04 LTS ISO</strong> file from the official website.</p>
<ol>
<li>Open your web browser and go to the official Ubuntu website: <a href="https://ubuntu.com/download/desktop">https://ubuntu.com/download/desktop</a>.</li>
<li>Click on <strong>Download 24.04.2 LTS</strong> to start the process.</li>
</ol>
<h3 id="step-2-download-and-install-rufus">Step 2: Download and Install Rufus</h3>
<p>To create a bootable USB drive, you will need <strong>Rufus</strong>, a tool designed for formatting and creating bootable USB drives.</p>
<ol>
<li>Go to the Rufus official website: <a href="https://rufus.ie">https://rufus.ie</a>.</li>
<li>Scroll down to the <strong>Download</strong> section.</li>
<li>Download the <strong>Standard</strong> version for your system architecture (<strong>x64</strong> in most cases).</li>
</ol>
<h3 id="step-3-create-a-bootable-usb">Step 3: Create a Bootable USB</h3>
<p>Now that you have both the Ubuntu ISO and Rufus installed, you can proceed with creating a bootable USB drive.</p>
<ol>
<li>Insert a USB drive (at least <strong>8GB</strong>) into your computer.</li>
<li>Run the <strong>Rufus</strong> executable to open it.</li>
<li>In the <strong>Device</strong> dropdown, select your USB drive.</li>
<li>Click <strong>Select</strong> and choose the <strong>Ubuntu 24.04.2 LTS ISO</strong> file you downloaded.</li>
<li>Set the <strong>Partition scheme</strong> to <strong>MBR</strong> and the <strong>Target system</strong> to <strong>BIOS or UEFI</strong>.</li>
<li>Under <strong>Format Options</strong>, set the <strong>File system</strong> to <strong>NTFS</strong> and the <strong>Cluster size</strong> to <strong>4096 bytes (Default)</strong>.</li>
<li>Click <strong>Start</strong>, a prompt will appear asking for the write mode—select <strong>Write in ISO Image mode (Recommended)</strong> and click <strong>OK</strong>, then wait for Rufus to create the bootable USB.</li>
<li>Once the process is complete, click <strong>Close</strong>.</li>
</ol>
<h3 id="step-4-shrink-the-disk-for-ubuntu">Step 4: Shrink the Disk for Ubuntu</h3>
<p>Before installing Ubuntu, you need to allocate space on your hard drive by shrinking an existing partition.</p>
<ol>
<li>Open <strong>Disk Management</strong> by right-clicking the Windows icon and selecting <strong>Disk Management</strong>.</li>
<li>Right-click the <strong>OS (C:)</strong> partition and select <strong>Shrink Volume</strong>.</li>
<li>In the pop-up window, enter the amount of space to shrink. The recommended space is <strong>400GB + 1.5× your RAM</strong> (for 16GB RAM: <strong>434,176MB</strong>) and click <strong>Shrink</strong>,.</li>
<li>You will see a new unallocated space in the disk.</li>
</ol>
<h3 id="step-5-boot-from-the-usb-drive">Step 5: Boot from the USB Drive</h3>
<p>To start the Ubuntu installation, you need to boot from the USB drive.</p>
<ol>
<li>Restart your computer and enter the <strong>BIOS/UEFI</strong> by pressing the designated key for your system brand:
<ul>
<li><strong>Dell</strong>: <code>F2</code> or <code>F12</code></li>
<li><strong>HP</strong>: <code>Esc</code> or <code>F10</code></li>
<li><strong>Lenovo</strong>: <code>F1</code>, <code>F2</code>, or <code>Novo Button</code> (small button next to power)</li>
<li><strong>ASUS</strong>: <code>F2</code> or <code>Del</code></li>
</ul>
</li>
<li>Once inside the BIOS/UEFI, locate the <strong>Boot Options</strong> or <strong>Boot Configuration</strong> section.</li>
<li>Disable <strong>Fast Boot</strong> to allow USB booting and change the <strong>Boot Order</strong> to prioritize the USB drive…</li>
<li>Save changes and exit the BIOS/UEFI. Your system will now boot from the USB drive.</li>
</ol>
<h3 id="step-6-install-ubuntu">Step 6: Install Ubuntu</h3>
<p>Now that your system has booted from the USB drive, follow these steps to install Ubuntu.</p>
<ol>
<li>On the welcome screen, select <strong>Try or Install Ubuntu</strong>.</li>
<li>Choose your <strong>language</strong>, configure <strong>Accessibility</strong> settings if needed, and select your <strong>Keyboard Layout</strong>, then click <strong>Next</strong>.</li>
<li>Choose your <strong>Wi-Fi network</strong>,  enter the password, and click <strong>Next</strong>.</li>
<li>If an update prompt appears, select <strong>Skip</strong>.</li>
<li>Click <strong>Install Ubuntu</strong>.</li>
<li>Select <strong>Interactive Installation</strong>, then choose <strong>Extended Selection</strong>.</li>
<li>Check the boxes for:
<ul>
<li><strong>Install third-party software for graphics and Wi-Fi hardware</strong></li>
<li><strong>Download and install support for additional media formats</strong></li>
</ul>
</li>
<li>Click <strong>Manual Installation</strong>.</li>
<li>Locate the <strong>Free Space</strong> entry (this should match the amount of space you shrank earlier) and click <strong>“+”</strong>.</li>
<li>Create a <strong>swap partition</strong>:</li>
</ol>
<pre><code>-   Size: **1.5× RAM** (for 16GB RAM: **24GB / 24,576MB**) or **2.0× RAM** (for 16GB RAM: **32GB / 32,768MB**)
-   Used as: **Swap area**
-   Click **OK**.
</code></pre>
<ol start="11">
<li>Select the remaining <strong>Free Space</strong>, click <strong>“+”</strong>, and configure:</li>
</ol>
<pre><code>-   Used as: **Ext4 journaling file system**
-   Mount point: **/** (root)
-   Click **OK**.
</code></pre>
<ol start="12">
<li>Click <strong>Next</strong>.</li>
<li>Enter your <strong>name</strong>, <strong>computer name</strong>, <strong>username</strong>, and <strong>password</strong>.</li>
<li>Leave <strong>Use Active Directory</strong> <strong>unchecked</strong> and click <strong>Next</strong>.</li>
<li>Select your <strong>time zone</strong>, click <strong>Next</strong>.</li>
<li>Click <strong>Install Now</strong> and wait for the process to complete.</li>
</ol>
<h3 id="step-6-restart-and-complete-installation">Step 6: Restart and Complete Installation</h3>
<ol>
<li>Once the installation finishes, remove the USB drive.</li>
<li>Click <strong>Restart Now</strong>.</li>
<li>After rebooting, the <strong>boot menu</strong> will appear with options for <strong>Ubuntu</strong> and <strong>Windows Boot Manager</strong>.</li>
<li>Select <strong>Ubuntu</strong> to log in and complete any additional setup.</li>
</ol>
<h2 id="c.-gaussian-splatting-nerfstudio-installation"><strong>C. Gaussian Splatting Nerfstudio Installation</strong></h2>
<p>In this section, we will <strong>guide you step by step</strong> to install <strong>Nerfstudio</strong> with <strong>Gaussian Splatting</strong> on <strong>Ubuntu 24.04</strong>. This process includes installing all necessary dependencies, setting up your environment, and ensuring your system meets the requirements for running <strong>Gaussian Splatting</strong> efficiently.</p>
<p>By the end of this section, you will have a <strong>fully functional setup</strong> capable of performing Gaussian Splatting for <strong>NeRF reconstruction</strong> and rendering.</p>
<h3 id="step-1-check-nvidia-drivers"><strong>Step 1: Check NVIDIA Drivers</strong></h3>
<p>Before proceeding, verify if NVIDIA drivers are installed and correctly configured on your system. Open a terminal and run the following commands:</p>
<pre class=" language-bash"><code class="prism  language-bash">nvidia-settings --version
<span class="token function">cat</span> /proc/driver/nvidia/version
</code></pre>
<ul>
<li>If these commands return a <strong>valid NVIDIA driver version</strong> and <strong>both versions match</strong>, proceed to <strong>Step 3: Install CUDA</strong>.</li>
<li>If they return an <strong>error</strong> or <strong>show different versions</strong>, proceed to <strong>Step 2: Install NVIDIA Drivers</strong>.</li>
</ul>
<h3 id="step-2-install-nvidia-drivers"><strong>Step 2: Install NVIDIA Drivers</strong></h3>
<ol>
<li><strong>Visit NVIDIA Driver Download Page</strong><br>
Go to the official NVIDIA driver page:<br>
<a href="https://www.nvidia.com/en-us/drivers/unix/">NVIDIA Driver Download</a></li>
<li><strong>Select the Driver</strong><br>
Search for the best driver for your GPU, or use a stable version like <strong>Latest New Feature Branch Version: 565.77</strong>. Select your driver version and click <strong>Download</strong>. This will download a <code>.run</code> file (e.g., <code>NVIDIA-Linux-x86_64-565.77.run</code>).</li>
<li><strong>Update and Upgrade</strong><br>
Open a terminal and run the following commands to ensure your system is up to date and to remove any existing NVIDIA drivers:</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> apt update
<span class="token function">sudo</span> apt upgrade -y
</code></pre>
<ul>
<li><strong>sudo apt update</strong>: Updates the list of available packages.</li>
<li><strong>sudo apt upgrade</strong>: Installs updates for installed packages.</li>
</ul>
<p>Then, remove any NVIDIA-related drivers or packages to avoid conflicts:</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> apt remove --purge <span class="token string">'^nvidia-.*'</span> -y
</code></pre>
<ul>
<li>This command removes all NVIDIA-related packages from your system, including drivers and associated files.</li>
</ul>
<p>Clean up any unnecessary packages:</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> apt autoremove -y
<span class="token function">sudo</span> apt update
</code></pre>
<ul>
<li>Removes dependencies that are no longer needed.</li>
</ul>
<ol start="4">
<li><strong>Install Build Tools</strong><br>
Next, install the required build tools needed to compile the NVIDIA drivers:</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> apt <span class="token function">install</span> -y build-essential
</code></pre>
<ul>
<li>This installs essential packages for compiling software, including compilers and libraries.</li>
</ul>
<ol start="5">
<li><strong>Switch to Multi-User Target</strong><br>
Switch to a multi-user target mode, which is a non-graphical mode that helps avoid conflicts during the driver installation:</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> systemctl isolate multi-user.target
</code></pre>
<ul>
<li>This command switches the system to a state where no graphical environment is running, which is recommended for installing the driver.</li>
</ul>
<ol start="6">
<li><strong>Login with User Credentials</strong><br>
Log in with your username and password.</li>
<li><strong>Navigate to Downloads Directory</strong><br>
Go to the directory where the <code>.run</code> file was downloaded.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">cd</span> Downloads/
</code></pre>
<ol start="8">
<li><strong>Make the NVIDIA Installer Executable</strong><br>
Grant execution permissions to the <code>.run</code> file.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">chmod</span> +x NVIDIA-Linux-x86_64-565.77.run
</code></pre>
<ul>
<li><code>chmod +x</code>: Makes the <code>.run</code> file executable.</li>
</ul>
<ol start="9">
<li><strong>Run the NVIDIA Installer</strong><br>
Install the NVIDIA driver by running the <code>.run</code> file.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> ./NVIDIA-Linux-x86_64-565.77.run
</code></pre>
<ol start="10">
<li><strong>Follow the Prompts</strong></li>
</ol>
<ul>
<li>When prompted, select <strong>NVIDIA proprietary</strong> drivers.</li>
<li>Press <strong>Yes</strong>, <strong>Ok</strong> or <strong>Continue Installation</strong> when asked to proceed.</li>
<li>If asked about rebuilding <strong>initramfs</strong>, select <strong>Rebuild Initramfs</strong>.</li>
<li>Finally reboot the system to start new programs which use the NVIDIA GPU(s)</li>
</ul>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> <span class="token function">reboot</span>
</code></pre>
<ol start="11">
<li><strong>Verify Installation Again</strong><br>
After completing the installation, verify that the NVIDIA drivers were installed correctly:</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash">nvidia-settings --version
<span class="token function">cat</span> /proc/driver/nvidia/version
nvidia-smi
</code></pre>
<ul>
<li>If these commands return a valid <strong>NVIDIA driver version</strong> and both versions match, proceed to <strong>Step 3: Install CUDA</strong>.</li>
<li>If the commands return an error or the versions do not match, <strong>repeat Step 2</strong>, starting from the <strong>Update and Upgrade</strong> section.</li>
</ul>
<h3 id="step-3-install-cuda"><strong>Step 3: Install CUDA</strong></h3>
<p>To install CUDA on Ubuntu 24.04, follow these steps:</p>
<ol>
<li><strong>Update the Package List</strong><br>
Ensure your system package list is up to date.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> apt update
</code></pre>
<ol start="2">
<li><strong>Download the CUDA Repository Pin</strong><br>
This file helps prioritize the CUDA repository during package installation.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">wget</span> https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-ubuntu2404.pin
</code></pre>
<ol start="3">
<li><strong>Move the Repository Pin</strong><br>
Place the downloaded pin file into the appropriate directory to apply its settings.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> <span class="token function">mv</span> cuda-ubuntu2404.pin /etc/apt/preferences.d/cuda-repository-pin-600
</code></pre>
<ol start="4">
<li><strong>Download the CUDA Repository Installer</strong><br>
Download the latest available CUDA installer for Ubuntu 24.04. The version used here is <strong>CUDA 12.8.1</strong>.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">wget</span> https://developer.download.nvidia.com/compute/cuda/12.8.1/local_installers/cuda-repo-ubuntu2404-12-8-local_12.8.1-570.124.06-1_amd64.deb
</code></pre>
<ol start="5">
<li><strong>Install the CUDA Repository</strong><br>
Use <code>dpkg</code> to install the downloaded package, which sets up the CUDA repository on your system.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> dpkg -i cuda-repo-ubuntu2404-12-8-local_12.8.1-570.124.06-1_amd64.deb
</code></pre>
<ol start="6">
<li><strong>Add the Repository Key</strong><br>
Copy the repository’s GPG key to ensure package authenticity and prevent security warnings.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> <span class="token function">cp</span> /var/cuda-repo-ubuntu2404-12-8-local/cuda-*-keyring.gpg /usr/share/keyrings/
</code></pre>
<ol start="7">
<li><strong>Update the Package List Again</strong><br>
Refresh the package list to include the newly added CUDA repository.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> <span class="token function">apt-get</span> update
</code></pre>
<ol start="8">
<li><strong>Install CUDA Toolkit</strong><br>
Install the CUDA Toolkit, which includes the CUDA compiler, libraries, and tools needed for development.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> <span class="token function">apt-get</span> -y <span class="token function">install</span> cuda-toolkit-12-8
</code></pre>
<ol start="9">
<li><strong>Install NVIDIA CUDA Toolkit</strong><br>
This package provides additional CUDA-related tools and dependencies.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> apt <span class="token function">install</span> nvidia-cuda-toolkit
</code></pre>
<ol start="10">
<li><strong>Verify CUDA Installation</strong><br>
Run <code>nvcc --version</code> to confirm that CUDA has been installed correctly.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash">nvcc --version
</code></pre>
<ul>
<li>If the output displays the <strong>NVIDIA CUDA compiler driver</strong> version (e.g., <strong>12.8.1</strong>), the installation was successful.</li>
<li>If the command returns an error, repeat the installation steps starting from the <strong>Update the Package List</strong> section.</li>
</ul>
<h3 id="step-4-install-docker"><strong>Step 4: Install Docker</strong></h3>
<p>To install Docker on Ubuntu 24.04, follow these steps:</p>
<ol>
<li><strong>Update and Upgrade Packages</strong><br>
Ensure your system is up to date before installing Docker.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> apt update <span class="token operator">&amp;&amp;</span> <span class="token function">sudo</span> apt upgrade -y
</code></pre>
<ol start="2">
<li><strong>Install Required Dependencies</strong><br>
Install essential packages for HTTPS-based repositories and certificate management.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> apt <span class="token function">install</span> apt-transport-https ca-certificates curl software-properties-common -y
</code></pre>
<ol start="3">
<li><strong>Add Docker’s Official GPG Key</strong><br>
Download and store Docker’s official signing key to verify package integrity.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash">curl -fsSL https://download.docker.com/linux/ubuntu/gpg <span class="token operator">|</span> <span class="token function">sudo</span> gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
</code></pre>
<ol start="4">
<li><strong>Add Docker Repository</strong><br>
Configure the system to use Docker’s stable repository for installation.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token keyword">echo</span> <span class="token string">"deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu <span class="token variable"><span class="token variable">$(</span>lsb_release -cs<span class="token variable">)</span></span> stable"</span> <span class="token operator">|</span> <span class="token function">sudo</span> <span class="token function">tee</span> /etc/apt/sources.list.d/docker.list <span class="token operator">&gt;</span> /dev/null
</code></pre>
<ol start="5">
<li><strong>Update the Package List</strong><br>
Refresh the package list to include the newly added Docker repository.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> apt update
</code></pre>
<ol start="6">
<li><strong>Install Docker Engine</strong><br>
Install Docker Community Edition (CE) along with essential components.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> apt <span class="token function">install</span> docker-ce docker-ce-cli containerd.io -y
</code></pre>
<ol start="7">
<li><strong>Verify Docker Installation</strong><br>
Run <code>docker --version</code> to confirm that Docker has been installed correctly.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> docker --version
</code></pre>
<pre><code>-   If the output displays a valid Docker version (e.g., **28.0.1**), the installation was successful.      
-   If the command returns an error, repeat the installation steps starting from **Update and Upgrade Packages**.
</code></pre>
<ol start="8">
<li><strong>Add Current User to Docker Group</strong><br>
Grant the current user permission to run Docker without <code>sudo</code>.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> <span class="token function">usermod</span> -aG docker <span class="token variable">$USER</span>
</code></pre>
<ol start="9">
<li><strong>Check Docker Service Status</strong><br>
Verify that Docker is running and active.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> systemctl status docker
</code></pre>
<ul>
<li>If Docker is <strong>active (running)</strong>, proceed to the next step.</li>
<li>If the service is inactive or shows errors, restart Docker using the steps above or refer to the <strong>Commands to Run Docker</strong> section in the annex.</li>
<li>If Docker is still inactive or returns an error, consider reinstalling Docker from <strong>Step 1</strong>.</li>
</ul>
<ol start="10">
<li><strong>Verify Docker Installation</strong><br>
Runs a test container to check if Docker is working properly.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> docker run hello-world
</code></pre>
<ol start="11">
<li><strong>List Installed Docker Images</strong><br>
Displays the list of available Docker images.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> docker images
</code></pre>
<ol start="12">
<li><strong>Pull NVIDIA CUDA Image</strong><br>
Downloads the <strong>NVIDIA CUDA 11.8.0 with cuDNN 8</strong> image for Ubuntu 22.04.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> docker pull nvidia/cuda:11.8.0-cudnn8-devel-ubuntu22.04
</code></pre>
<ol start="13">
<li><strong>Verify CUDA Image Installation</strong><br>
Lists all downloaded images to confirm that the CUDA image is available.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> docker images
</code></pre>
<ul>
<li>If <code>nvidia/cuda:11.8.0-cudnn8-devel-ubuntu22.04</code> appears in the list, the installation was successful.</li>
<li>If the image is missing, repeat the <strong>Pull NVIDIA CUDA Image</strong> step.</li>
</ul>
<p>If the image is listed, you can continue with the next step of the installation: <strong>Setting Up the Docker Container</strong>.</p>
<h3 id="step-5-setting-up-the-docker-container"><strong>Step 5: Setting Up the Docker Container</strong></h3>
<p>To configure the Docker container with NVIDIA support, follow these steps:</p>
<p>The first step in setting up the Docker container is installing the <strong>NVIDIA Container Toolkit</strong>, which enables GPU support for containers.</p>
<ol>
<li><strong>Update and Upgrade Packages</strong><br>
Ensure the system is updated to prevent conflicts during installation.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> apt update
</code></pre>
<ol start="2">
<li><strong>Add NVIDIA Repository for Container Toolkit</strong><br>
Add the official NVIDIA repository to install the necessary container tools.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash">curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey <span class="token operator">|</span> <span class="token function">sudo</span> gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg
curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list <span class="token operator">|</span> \
<span class="token function">sed</span> <span class="token string">'s#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g'</span> <span class="token operator">|</span> \
<span class="token function">sudo</span> <span class="token function">tee</span> /etc/apt/sources.list.d/nvidia-container-toolkit.list
</code></pre>
<ol start="3">
<li><strong>Update the Package List</strong><br>
Refresh the package list to include the newly added NVIDIA repository.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> <span class="token function">apt-get</span> update
</code></pre>
<ol start="4">
<li><strong>Install NVIDIA Container Toolkit</strong><br>
Install the required toolkit to enable GPU support in Docker containers.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> <span class="token function">apt-get</span> <span class="token function">install</span> -y nvidia-container-toolkit
</code></pre>
<ol start="5">
<li><strong>Configure NVIDIA Runtime for Containerd</strong><br>
Set up the NVIDIA runtime to work with <strong>containerd</strong>, ensuring GPU acceleration in containers.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> nvidia-ctk runtime configure --runtime<span class="token operator">=</span>docker
</code></pre>
<ol start="6">
<li><strong>Restart Docker</strong><br>
Apply the changes by restarting the Docker service.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> systemctl restart docker
</code></pre>
<ol start="7">
<li><strong>Install NVIDIA Docker Support</strong><br>
Install <strong>nvidia-docker2</strong>, which integrates the NVIDIA runtime into Docker.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> <span class="token function">apt-get</span> <span class="token function">install</span> -y nvidia-docker2
</code></pre>
<p>If you’re not familiar with the main Docker commands, please refer to the <strong>Docker Usage Commands</strong> section in the annex for a detailed guide on how to use Docker effectively.<br>
8.  <strong>Run the Container with NVIDIA GPU Support</strong><br>
After installing <strong>nvidia-docker2</strong>, you can run the container with GPU support using the command:</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> docker run --cpus<span class="token operator">=</span>8 --memory<span class="token operator">=</span>11g --memory-swap<span class="token operator">=</span>17g --shm-size<span class="token operator">=</span>6g --runtime<span class="token operator">=</span>nvidia --gpus all -it --rm nvidia/cuda:11.8.0-cudnn8-devel-ubuntu22.04
</code></pre>
<ul>
<li><code>--cpus=8</code> → Limits the container to use only 8 CPU cores.</li>
<li><code>--memory=11g</code> → Allocates 11GB of RAM to the container.</li>
<li><code>--memory-swap=17g</code> → Sets the total memory limit (RAM + Swap) to 17GB.</li>
<li><code>--shm-size=6g</code> → Increases the shared memory allocation to 6GB, useful for PyTorch and other memory-intensive processes.</li>
<li><code>--runtime=nvidia --gpus all</code> → Ensures the container has access to the GPU for accelerated computation.</li>
</ul>
<ol start="9">
<li><strong>Install Miniconda</strong><br>
If conda is not installed within the container, follow these steps to install it:</li>
</ol>
<ul>
<li>First, check the version of conda:<pre class=" language-bash"><code class="prism  language-bash">conda --version
</code></pre>
If the command is not found, proceed with the installation.</li>
<li>Update and install necessary packages:<pre class=" language-bash"><code class="prism  language-bash">apt update <span class="token operator">&amp;&amp;</span> apt <span class="token function">install</span> <span class="token function">wget</span> -y
apt upgrade -y
</code></pre>
</li>
<li>Download and install Miniconda:<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">wget</span> https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
<span class="token function">bash</span> Miniconda3-latest-Linux-x86_64.sh

</code></pre>
Follow the on-screen instructions and press ENTER. Type <strong>yes</strong> when prompted to proceed with the installation.</li>
<li>After installation, source the bashrc to refresh the shell environment:<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">source</span> ~/.bashrc
</code></pre>
</li>
<li>Finally, verify that conda is properly installed:<pre class=" language-bash"><code class="prism  language-bash">conda --version
</code></pre>
You should see the version number of conda (e.g., <code>conda 25.1.1</code>).<br>
It is recommended to make a commit after each step from here on out. This will allow you to save the changes made without committing to the container. The steps to do this include: listing the containers, obtaining the container ID, making a commit, and removing the oldest image. These commands are detailed in the <strong>Docker Usage Commands</strong> section in the annex.</li>
</ul>
<ol start="10">
<li><strong>Create and Activate the Conda Environment</strong></li>
</ol>
<ul>
<li>Create a new Conda environment called <code>nerfstudio</code> with Python 3.8<pre class=" language-bash"><code class="prism  language-bash">conda create --name nerfstudio -y python<span class="token operator">=</span>3.8
</code></pre>
</li>
<li>Activate the environment<pre class=" language-bash"><code class="prism  language-bash">conda activate nerfstudio
</code></pre>
</li>
</ul>
<ol start="11">
<li><strong>Install Specific Versions of PyTorch and torchvision</strong></li>
</ol>
<ul>
<li>Upgrade pip to the latest version within the <code>nerfstudio</code> environment<pre class=" language-bash"><code class="prism  language-bash">python -m pip <span class="token function">install</span> --upgrade pip
</code></pre>
</li>
<li>Uninstall existing versions of <code>torch</code>, <code>torchvision</code>, <code>functorch</code>, and <code>tinycudann</code><pre class=" language-bash"><code class="prism  language-bash">pip uninstall torch torchvision functorch tinycudann
</code></pre>
</li>
<li>Install the required versions of PyTorch and torchvision compatible with CUDA 11.8:<pre class=" language-bash"><code class="prism  language-bash">pip <span class="token function">install</span> torch<span class="token operator">==</span>2.1.2+cu118 torchvision<span class="token operator">==</span>0.16.2+cu118 --extra-index-url https://download.pytorch.org/whl/cu118
</code></pre>
</li>
<li>Verify CUDA availability with PyTorch<pre class=" language-bash"><code class="prism  language-bash">python -c <span class="token string">"import torch; print(torch.cuda.is_available())"</span>
</code></pre>
</li>
</ul>
<ol start="12">
<li><strong>Install CUDA Toolkit</strong></li>
</ol>
<ul>
<li>Install the CUDA Toolkit version 11.8.0 from the NVIDIA channel using Conda<pre class=" language-bash"><code class="prism  language-bash">conda <span class="token function">install</span> -c <span class="token string">"nvidia/label/cuda-11.8.0"</span> cuda-toolkit -y
</code></pre>
</li>
<li>Verify that the correct CUDA toolkit is installed<pre class=" language-bash"><code class="prism  language-bash">conda list <span class="token operator">|</span> <span class="token function">grep</span> cuda
</code></pre>
</li>
</ul>
<ol start="13">
<li><strong>Install Ninja</strong><br>
Install <code>ninja</code>, a small build system, which is required for building certain dependencies</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash">pip <span class="token function">install</span> ninja
</code></pre>
<ol start="14">
<li><strong>Install Tiny CUDA NN</strong></li>
</ol>
<ul>
<li>Update the package list and install <code>git</code><pre class=" language-bash"><code class="prism  language-bash"><span class="token function">apt-get</span> update
<span class="token function">apt-get</span> <span class="token function">install</span> <span class="token function">git</span> -y
</code></pre>
</li>
<li>Install the <code>tiny-cuda-nn</code> library from GitHub using <code>pip</code><pre class=" language-bash"><code class="prism  language-bash">pip <span class="token function">install</span> git+https://github.com/NVlabs/tiny-cuda-nn/<span class="token comment">#subdirectory=bindings/torch</span>
</code></pre>
</li>
<li>Verify the installation of <code>tiny-cuda-nn</code>:<pre class=" language-bash"><code class="prism  language-bash">python -c <span class="token string">"import tinycudann; print('tiny-cuda-nn is installed')"</span>
</code></pre>
</li>
</ul>
<ol start="15">
<li><strong>Install Pixi</strong></li>
</ol>
<ul>
<li>Update the package list<pre class=" language-bash"><code class="prism  language-bash">apt update
</code></pre>
</li>
<li>Install <code>curl</code><pre class=" language-bash"><code class="prism  language-bash">apt <span class="token function">install</span> curl -y
</code></pre>
</li>
<li>Download and run the Pixi installer<pre class=" language-bash"><code class="prism  language-bash">curl -fsSL https://pixi.sh/install.sh <span class="token operator">|</span> <span class="token function">bash</span>
</code></pre>
</li>
<li>Source the bashrc to refresh the shell environment<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">source</span> ~/.bashrc
</code></pre>
</li>
<li>Verify the Pixi version<pre class=" language-bash"><code class="prism  language-bash">pixi --version
</code></pre>
</li>
</ul>
<ol start="16">
<li><strong>Clone Nerfstudio Repository</strong></li>
</ol>
<ul>
<li>Clone the <code>nerfstudio</code> repository from GitHub<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">git</span> clone https://github.com/nerfstudio-project/nerfstudio.git
</code></pre>
</li>
<li>Navigate into the <code>nerfstudio</code> directory<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">cd</span> nerfstudio
</code></pre>
</li>
</ul>
<ol start="17">
<li><strong>Run Post-Install Script and Start Pixi</strong></li>
</ol>
<ul>
<li>Run the post-install script for Nerfstudio<pre class=" language-bash"><code class="prism  language-bash">pixi run post-install
</code></pre>
</li>
<li>Start the Pixi shell<pre class=" language-bash"><code class="prism  language-bash">pixi shell
</code></pre>
</li>
</ul>
<ol start="18">
<li><strong>Run Nerfstudio Example</strong></li>
</ol>
<ul>
<li>Update the package list<pre class=" language-bash"><code class="prism  language-bash">apt update
</code></pre>
</li>
<li>Install the <code>libgl1-mesa-glx</code> package, which is required for rendering<pre class=" language-bash"><code class="prism  language-bash">apt <span class="token function">install</span> libgl1-mesa-glx -y
</code></pre>
</li>
<li>Execute the <code>train-example-nerf</code> to verify if everything is working correctly<pre class=" language-bash"><code class="prism  language-bash">pixi run train-example-nerf
</code></pre>
</li>
<li>Use ns-viewer to load the configuration and visualize the output of the training. Check the filename in outputs/dozer/nerfacto.<pre class=" language-bash"><code class="prism  language-bash">ns-viewer --load-config outputs/dozer/nerfacto/2025-03-10_141612/config.yml
</code></pre>
</li>
<li>Once the viewer is running, open a web browser and enter the following URL:**<pre class=" language-bash"><code class="prism  language-bash">http://0.0.0.0:7007
</code></pre>
</li>
<li><strong>Important:</strong> Replace <code>0.0.0.0</code> with the actual IP address of your container. You can find it using:<pre class=" language-bash"><code class="prism  language-bash">docker inspect container_id <span class="token operator">|</span> <span class="token function">grep</span> <span class="token string">"IPAddress"</span>
</code></pre>
</li>
</ul>
<ol start="19">
<li><strong>Install and Verify GSplat</strong></li>
</ol>
<ul>
<li>Install <code>gsplat</code> using <code>pip</code><pre class=" language-bash"><code class="prism  language-bash">pip <span class="token function">install</span> gsplat
</code></pre>
</li>
<li>Install the latest version of <code>gsplat</code> directly from GitHub<pre class=" language-bash"><code class="prism  language-bash">pip <span class="token function">install</span> git+https://github.com/nerfstudio-project/gsplat
</code></pre>
</li>
<li>Check if <code>gsplat</code> is installed correctly<pre class=" language-bash"><code class="prism  language-bash">python -c <span class="token string">"import gsplat; print('gsplat installed successfully')"</span>
</code></pre>
</li>
</ul>
<ol start="20">
<li><strong>Copy Video File to Container</strong></li>
</ol>
<ul>
<li><strong>Note:</strong> <code>pista.mp4</code> is a test video. You can download it from the following link:<br>
<strong>[<a href="https://drive.google.com/file/d/1JQCOZGtHDf9HyXCcjiQpW29SAT-4_9O4/view?usp=sharing">https://drive.google.com/file/d/1JQCOZGtHDf9HyXCcjiQpW29SAT-4_9O4/view?usp=sharing</a>]</strong></li>
<li>Replace it with the actual path to your test video (e.g., <code>path/to/your/test/video</code>).</li>
<li>Copy the video file to the container using the <code>docker cp</code> command. Replace <code>container_id</code> with your container’s ID:<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> docker <span class="token function">cp</span> /home/genaro-rivero/Downloads/pista.MP4 container_id:/root/nerfstudio
</code></pre>
</li>
</ul>
<ol start="21">
<li><strong>Process Video Data</strong></li>
</ol>
<ul>
<li>Run the <code>ns-process-data</code> command to process the video file. Replace <code>./pista.MP4</code> with the correct path inside the container<pre class=" language-bash"><code class="prism  language-bash">ns-process-data video --data ./pista.MP4 --sfm-tool hloc --output-dir ./processed
</code></pre>
</li>
</ul>
<ol start="22">
<li><strong>Train Model with Processed Data</strong><br>
<strong>Note:</strong> If you previously installed Ubuntu and encounter memory-related issues at this step, refer to the <strong>Annex: Memory Usage Issues</strong> for troubleshooting.</li>
</ol>
<ul>
<li>Start training the model using the processed data. Adjust the command as needed<pre class=" language-bash"><code class="prism  language-bash">ns-train splatfacto --pipeline.model.cull_alpha_thresh<span class="token operator">=</span>0.005 --pipeline.model.stop-screen-size-at<span class="token operator">=</span>15000 --pipeline.model.use_scale_regularization<span class="token operator">=</span>True --data ./processed
</code></pre>
</li>
</ul>
<ol start="23">
<li><strong>View the Training Output</strong></li>
</ol>
<ul>
<li>Use <code>ns-viewer</code> to visualize the results of the training. Check the filename in outputs/processed/splatfacto.<pre class=" language-bash"><code class="prism  language-bash">ns-viewer --load-config outputs/processed/splatfacto/2025-03-11_210124/config.yml`
</code></pre>
</li>
<li>Once the viewer is running, open a web browser and enter the following URL:**<pre class=" language-bash"><code class="prism  language-bash">http://0.0.0.0:7007
</code></pre>
</li>
<li><strong>Important:</strong> Replace <code>0.0.0.0</code> with the actual IP address of your container. You can find it using:<pre class=" language-bash"><code class="prism  language-bash">docker inspect container_id <span class="token operator">|</span> <span class="token function">grep</span> <span class="token string">"IPAddress"</span>
</code></pre>
</li>
</ul>
<h2 id="annex"><strong>Annex</strong></h2>
<h3 id="commands-to-run-docker"><strong>Commands to Run Docker</strong></h3>
<ol>
<li><strong>Stop Docker</strong><br>
This command stops the Docker service.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> systemctl stop docker
</code></pre>
<ol start="2">
<li><strong>Start Docker</strong><br>
This command starts the Docker service again.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> systemctl start docker
</code></pre>
<ol start="3">
<li><strong>Restart Docker</strong><br>
This command restarts Docker in a single step.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> systemctl restart docker
</code></pre>
<ol start="4">
<li><strong>Check Docker Status Again</strong><br>
Ensure that Docker is now <strong>active (running)</strong>.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> systemctl status docker
</code></pre>
<h3 id="docker-usage-commands">Docker Usage Commands</h3>
<ol>
<li><strong>List Docker Images</strong><br>
This command allows you to view all available images on your system.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> docker images
</code></pre>
<ol start="2">
<li><strong>List Running Containers</strong><br>
This command shows the containers that are currently running. You can also view all containers, including stopped ones.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> docker <span class="token function">ps</span> -a
</code></pre>
<ol start="3">
<li><strong>Remove a Container</strong><br>
To remove a stopped container, this command can be used. Additionally, there’s a command to remove all stopped containers at once.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> docker <span class="token function">rm</span> <span class="token variable"><span class="token variable">$(</span><span class="token function">sudo</span> docker <span class="token function">ps</span> -a -q<span class="token variable">)</span></span>
</code></pre>
<ol start="4">
<li><strong>Remove an Image</strong><br>
This command allows you to remove a Docker image from your system.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> docker rmi <span class="token operator">&lt;</span>image_id<span class="token operator">&gt;</span>
</code></pre>
<ol start="5">
<li><strong>Commit Changes from a Container to a New Image</strong><br>
If you’ve made changes to a container and want to save those changes as a new image, this command will help you do that.</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> docker commit <span class="token operator">&lt;</span>container_id<span class="token operator">&gt;</span> <span class="token operator">&lt;</span>new_image_name<span class="token operator">&gt;</span>:<span class="token operator">&lt;</span>tag<span class="token operator">&gt;</span>
</code></pre>
<ol start="6">
<li><strong>Run a Container with GPU Support</strong><br>
If your system is configured to use NVIDIA GPUs, you can run a container with GPU support, allowing you to take advantage of GPU acceleration in your applications</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> docker run --rm --gpus all <span class="token operator">&lt;</span>image_name<span class="token operator">&gt;</span> <span class="token operator">&lt;</span>command<span class="token operator">&gt;</span>
</code></pre>
<h3 id="memory-usage-issues"><strong>Memory Usage Issues</strong></h3>
<p>If the training process is not progressing or your laptop becomes unresponsive (e.g., the cursor stops moving), it is likely due to the high memory requirements of the training. This can happen when:</p>
<ul>
<li><strong>Insufficient RAM</strong> is available</li>
<li><strong>Low Swap Memory Allocation</strong> during the installation process.</li>
<li><strong>Shared Memory (shm) is too small</strong>, limiting the container’s available memory.<br>
To prevent these issues, allocate a sufficient amount of memory when running the container.</li>
</ul>
<hr>
<h4 id="assigning-more-memory-to-the-container"><strong>Assigning More Memory to the Container</strong></h4>
<p>If your system struggles with training, try running the container with a specific amount of CPU and memory allocation.</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> docker run --cpus<span class="token operator">=</span>8 --memory<span class="token operator">=</span>11g --memory-swap<span class="token operator">=</span>17g --shm-size<span class="token operator">=</span>6g --runtime<span class="token operator">=</span>nvidia --gpus all -it --rm nvidia/cuda:11.8.0-cudnn8-devel-ubuntu22.04
</code></pre>
<ul>
<li>
<p><strong>Explanation of Each Parameter:</strong></p>
<ul>
<li><code>--cpus=8</code> → Limits the container to use only 8 CPU cores.</li>
<li><code>--memory=11g</code> → Allocates 11GB of RAM to the container.</li>
<li><code>--memory-swap=17g</code> → Sets the total memory limit (RAM + Swap) to 17GB.</li>
<li><code>--shm-size=6g</code> → Increases the shared memory allocation to 6GB, useful for PyTorch and other memory-intensive processes.</li>
<li><code>--runtime=nvidia --gpus all</code> → Ensures the container has access to the GPU for accelerated computation.<br>
If reducing the assigned memory does not resolve the issue and the system still becomes unresponsive (e.g., the cursor stops moving), proceed to the next section.</li>
</ul>
</li>
</ul>
<hr>
<h4 id="checking-system-memory-and-cpu-usage"><strong>Checking System Memory and CPU Usage</strong></h4>
<p>Before adjusting additional settings, check the current memory and CPU availability with the following steps:</p>
<ul>
<li>Check available RAM and swap memory. This will show the total, used, and available RAM and swap memory in a human-readable format.</li>
</ul>
<pre class=" language-bash"><code class="prism  language-bash">`free -h
</code></pre>
<ul>
<li>Check shared memory (shm) allocation. If the size is too low, you may need to increase it.</li>
</ul>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">df</span> -h <span class="token operator">|</span> <span class="token function">grep</span> shm
</code></pre>
<ul>
<li>Check the number of available CPU cores. The number of processor cores available can affect training performance.</li>
</ul>
<pre class=" language-bash"><code class="prism  language-bash">nproc
</code></pre>
<ul>
<li>Monitor memory usage in real time. Continuously updating the memory status can help track usage during training.</li>
</ul>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">watch</span> -n 1 <span class="token function">free</span> -h
</code></pre>
<hr>
<h4 id="optimizing-pytorch-and-gsplat-performance"><strong>Optimizing PyTorch and Gsplat Performance</strong></h4>
<p>If the problem persists, modify PyTorch and Gsplat settings to optimize memory usage.</p>
<ol>
<li><strong>Increase matrix multiplication precision</strong><br>
Navigate to the PyTorch compiler directory</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">cd</span> .pixi/envs/default/lib/python3.10/site-packages/torch/_inductor/
</code></pre>
<p>Edit the file <code>compile_fx.py</code>.</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">nano</span> compile_fx.py
</code></pre>
<p>Inside the file, add a line to optimize matrix multiplications by increasing precision.</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">import</span> torch
torch<span class="token punctuation">.</span>set_float32_matmul_precision<span class="token punctuation">(</span><span class="token string">'high'</span><span class="token punctuation">)</span>
</code></pre>
<ol start="2">
<li><strong>Modify gsplat backend settings</strong><br>
Navigate to the gsplat CUDA backend directory</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">cd</span> .pixi/envs/default/lib/python3.10/site-packages/gsplat/cuda/
</code></pre>
<p>Edit <code>_backend.py</code>.</p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">nano</span> _backend.py
</code></pre>
<p>Modify the script to adjust job allocation, limiting the number of parallel jobs to prevent excessive memory usage.</p>
<pre class=" language-python"><code class="prism  language-python">PATH <span class="token operator">=</span> os<span class="token punctuation">.</span>path<span class="token punctuation">.</span>dirname<span class="token punctuation">(</span>os<span class="token punctuation">.</span>path<span class="token punctuation">.</span>abspath<span class="token punctuation">(</span>__file__<span class="token punctuation">)</span><span class="token punctuation">)</span>
NO_FAST_MATH <span class="token operator">=</span> os<span class="token punctuation">.</span>getenv<span class="token punctuation">(</span><span class="token string">"NO_FAST_MATH"</span><span class="token punctuation">,</span> <span class="token string">"0"</span><span class="token punctuation">)</span> <span class="token operator">==</span> <span class="token string">"1"</span>
MAX_JOBS <span class="token operator">=</span> os<span class="token punctuation">.</span>getenv<span class="token punctuation">(</span><span class="token string">"MAX_JOBS"</span><span class="token punctuation">)</span>
need_to_unset_max_jobs <span class="token operator">=</span> <span class="token boolean">False</span>
<span class="token keyword">if</span> <span class="token operator">not</span> MAX_JOBS<span class="token punctuation">:</span>
 need_to_unset_max_jobs <span class="token operator">=</span> <span class="token boolean">True</span>
 os<span class="token punctuation">.</span>environ<span class="token punctuation">[</span><span class="token string">"MAX_JOBS"</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"5"</span>
</code></pre>
<p>By following these steps, you can improve system stability and allow the training process to complete successfully.</p>

