# DaVinci Resolve 18.0 for Linux

DaVinci Resolve 18 is a major release featuring cloud-based collaboration, new AI tools, and a faster engine. It is the world’s only solution that combines editing, color correction, visual effects, motion graphics, and audio post-production all in one software tool!

---

## 📸 Interface & Visuals

![DaVinci Resolve Interface](https://imgs.search.brave.com/dLKw_9Q4VCHH5Om79NxebMQkpj9Iw3oVIOTbadWdGjA/rs:fit:500:0:1:0/g:ce/aHR0cHM6Ly9zYi13/cC1hc3NldHMuc3Rv/cnlibG9ja3MuY29t/L3Jlc291cmNlcy93/cC1jb250ZW50L3Vw/bG9hZHMvMjAyNC8w/Ni8yNzEwMzIzMS8w/My1NZWRpYS1QYWdl/LTEwMjR4NTU2LnBu/Zw)

*Professional editing and color grading workspace.*

![Color Grading](https://imgs.search.brave.com/KSVtrZ9cQG6IYNWbxoGs_N6JZ7OA00JNQoAxjbznFyw/rs:fit:500:0:1:0/g:ce/aHR0cHM6Ly93d3cu/YWRvcmFtYS5jb20v/YWxjL3dwLWNvbnRl/bnQvdXBsb2Fkcy8y/MDI1LzA4L3F1YWxp/Zmllci1zY2FsZWQt/MS0xMDI0eDQxMy5q/cGc)

*Advanced HDR color correction tools.*

---

## ✨ Key Features

*   **Blackmagic Cloud:** Host project libraries on DaVinci Resolve Project Server in the cloud.
*   **Blackmagic Proxy Generator:** Automatically creates and manages proxies from camera originals.
*   **Magic Mask:** AI-powered object masking to track and isolate specific subjects.
*   **Depth Map:** Automatically generate a 3D depth matte of a scene for rapid grading.
*   **Surface Tracker:** Track graphics onto surfaces that change perspective or warp.
*   **Voice Isolation:** AI-based tool to remove loud, unwanted noise from voice recordings.
*   **Fairline Audio:** Professional tools for audio post-production and mastering.

---

## 🛠 System Requirements (Linux)

*   **OS:** Rocky Linux 8.6 or CentOS 7.3 (and compatible distros).
*   **if you use any debian destro** most be install MakeResolveDeb
*   ![MakeResolveDeb](https://www.danieltufvesson.com/images/header_makeresolvedeb.png)
                       [![Download MakeResolveDeb](https://imgs.search.brave.com/pVXskIw0IVeW_aJCZPFm_gSfHjLTpaYtj49kUkF-8X8/rs:fit:500:0:1:0/g:ce/aHR0cHM6Ly9jZG4u/cGl4YWJheS5jb20v/cGhvdG8vMjAxNi8w/Mi8wOC8xOS81Mi9i/dXR0b24tMTE4NzQ2/MF82NDAucG5n)](https://www.danieltufvesson.com/download/?file=makeresolvedeb/makeresolvedeb_1.9.0_multi.sh.tar.gz)


[![Install DaVinci Resolve 18 On Debian](https://youtu.be/uxdyC3h5zbY)](https://youtu.be/uxdyC3h5zbY)


Download MakeResolveDeb
Download the latest version of the MakeResolveDeb *.tar.gz archive from this website and put it in the same directory as the Resolve installer *.zip archive.
=====
```
cd ~/resolvedeb
unzip DaVinci_Resolve_Studio_18_Linux.zip
tar zxvf makeresolvedeb_1.7.2_multi.sh.tar.gz
```
====
You should now have the following files in the directory:
```
DaVinci_Resolve_Studio_18_Linux.run
DaVinci_Resolve_Studio_18_Linux.zip
Linux_Installation_Instructions.pdf
makeresolvedeb_1.7.2_multi.sh.tar.gz
makeresolvedeb_1.7.2_multi.sh
```
### Run MakeResolveDeb

When you have unpacked the archives and have all the needed files in the directory it's time to assemble the new *.deb file using MakeResolveDeb. First install required packages.
```
sudo apt-get install fakeroot
```
### For Resolve 15.x you also need xorriso:
```
sudo apt-get install xorriso
```
The current version of MakeResolveDeb works for both Resolve and Resolve Studio. MakeResolveDeb will detect the Resolve variant in the archive and generate the appropriate Debian package. Run MakeResolveDeb and give the DaVinci Resolve installer *.run archive file name as the only argument.

For example:
```
./makeresolvedeb_1.7.2_multi.sh DaVinci_Resolve_Studio_19_Linux.run
```

The conversion can take a few minutes depending on computer and storage performance. If there are errors during the process it will be displayed on the terminal. A successful conversion is indicated by the last line saying "[DONE]" and the reported number of errors 0.

NOTE: MakeResolveDeb will store temporary data in the working directory. Make sure you have enough space available on the filesystem used for the conversion (approximately 4x the size of the downloaded archive).


### Installing the Debian package
A successful conversion generates a *.deb file that can be installed to your system. To install Resolve you can use dpkg.

For example:

```
sudo dpkg -i davinci-resolve-studio_19-mrd1.7.2_amd64.deb
```
## or 
```
sudo dpkg -i davinci-resolve_19-mrd1.7.2_amd64.deb
```
You will have to make sure that you have all the driver packages installed that are required by Resolve. The GPU choice and GPU driver setup varies depending on the system. Use the latest available driver for your system. For NVIDIA and Debian it will be something like this:
```
sudo apt-get install nvidia-driver nvidia-opencl-icd libcuda1 libglu1-mesa
```
For h.264 and h.265 export you also need the NVIDIA encode library:
```
sudo apt-get install libnvidia-encode1
```

Also make sure there is only one OpenCL ICD installed. This can be verified by looking in the directory /etc/OpenCL/vendors/. There should be one and only one *.icd file there. For NVIDIA it will usually be called nvidia.icd.

Even if you plan to run CUDA you need to have OpenCL installed.

The current Debian driver situation for AMD/Radeon is unpolished to put it mildly and it's not packaged properly for Debian. Installation method for AMD/Radeon will be left as an exercise to the reader. You will need the amdgpu-pro driver with OpenCL support.

Running Resolve using an Intel GPU under Linux is not supported.

Upgrading Resolve
When there are new updates to Resolve or MakeResolveDeb you only need to repeat the process above. There is no need to uninstall any previous Resolve versions when upgrading as long as both versions are using MakeResolveDeb. The Debian package will take care of the upgrade for you.

Switching between Resolve and Resolve Studio may require you to first uninstall the existing package and then install the new package. It is not possible to accidentally install both packages.

Settings and user data will be retained when upgrading, but always make sure you have proper backups of your projects before making any changes.


Uninstalling Resolve
To uninstall Resolve you should use the Debian package manager. Do not start deleting directories manually or use the official (un)installer.

Uninstall DaVinci Resolve:
```
sudo apt-get remove davinci-resolve
```
Uninstall DaVinci Resolve Studio:
```
sudo apt-get remove davinci-resolve-studio
```


    
*   **RAM:** 32 GB minimum.
*   **GPU:** Discrete GPU with at least 4GB of VRAM (NVIDIA/AMD).
*   **Drivers:** NVIDIA Driver version 465.31 or newer.

---

## 📥 Download Installation File

Click the button below to download the DaVinci Resolve 18.0 Linux ZIP package:

[![Download DaVinci Resolve](https://imgs.search.brave.com/pVXskIw0IVeW_aJCZPFm_gSfHjLTpaYtj49kUkF-8X8/rs:fit:500:0:1:0/g:ce/aHR0cHM6Ly9jZG4u/cGl4YWJheS5jb20v/cGhvdG8vMjAxNi8w/Mi8wOC8xOS81Mi9i/dXR0b24tMTE4NzQ2/MF82NDAucG5n)](https://swr.cloud.blackmagicdesign.com/DaVinciResolve/v18.0/DaVinci_Resolve_18.0_Linux.zip?verify=1778097090-KcPWi%2BH6wmFzYEzwk2qc6jecMlfXY20gE9G%2BkvYjTKw%3D)
