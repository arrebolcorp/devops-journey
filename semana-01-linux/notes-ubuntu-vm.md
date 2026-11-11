##What is a distribution?
Is an operating system composed of the Linux Kernel, GNU tools, additional software and package manager. It may also also display server and desktop environment to be used as a regular OS.
The term distribution in Linux is because an entity like Ubuntu or Debian 'distributes' the linux kernel with all the necessary software and utilities (like network manager, package manager, desktop manager, e.t.c.) so that it can be used as a OS.

##What does LTS mean?
LTS means Long-Term Support, is a release with along sopport window.

##What do Guest Additions do?
Guest Additions is an external package designed to be installed inside a VirtualBox guest OS. It enables closer integration between the host and guest OSes, including features such as shared folder, custom video drivers, seamless window mode, and more.

##My first VM on this course:

1. I configured the vHardware. In this case in the next SS show my configuration.
<img width="434" height="375" alt="image" src="https://github.com/user-attachments/assets/17a680c5-9e65-4b19-b0e3-9b19e28d64bb" />

2. Her I show my version and uname.
<img width="1279" height="799" alt="image" src="https://github.com/user-attachments/assets/21f0bbee-e35c-464b-807e-c39943514ef3" />

3.Here, I use 'sudo apt update' for refreshes the list of available packages.
<img width="638" height="374" alt="image" src="https://github.com/user-attachments/assets/1d7b0dd2-c463-47b2-b190-f6950293819e" />

4. In the next one, "I use build -essential" for brings the compiler "dkm" to rebuilds modules when the kernel changes and "linux-headers-$(uname -r)" to feaches the headers that match your running kernel (uname -r prinst ist version).
<img width="638" height="374" alt="image" src="https://github.com/user-attachments/assets/5387cc35-2d23-4f77-88f9-53c12ed3e3f5" />
<img width="639" height="376" alt="image" src="https://github.com/user-attachments/assets/7017e3d1-c475-41d4-9d8d-e734cc64d8ad" />

5. For the end of this lesson, I installed a VirtualBox Guest Addiotions on my Ubuntu. Why? Because, VirtualBox Guest Aditions is a set of tools that improve your working experience between the Host and Guest machine. With these, I can transfer files between both these machines and also features like adaptive display and clipboard sharing. When completed the installation to next is reboot using "sudo reboot"
<img width="637" height="374" alt="image" src="https://github.com/user-attachments/assets/8bca283e-ec9b-4ee3-ab07-d3471cff8c82" />

6. After install the VirtualBox Guest Addtions I gonna configurate a Shared Clipboard and Drag and Drop (after is important execute a autorush.sh from VBox_GAs_7.x.x as a software).
<img width="636" height="373" alt="image" src="https://github.com/user-attachments/assets/be1e008b-a5e7-4bbd-8405-7c5b79a67684" />
<img width="640" height="377" alt="image" src="https://github.com/user-attachments/assets/ea228323-90f5-48d2-9ede-b6657345069a" />
<img width="527" height="296" alt="image" src="https://github.com/user-attachments/assets/592db213-f16c-4e90-b668-4e3864692352" />

7. If you have configurate a password to share files in the guest you can use this line 'sudo gpasswd --add $USER vboxsf'
<img width="1279" height="745" alt="image" src="https://github.com/user-attachments/assets/03271c1c-35b3-440d-a8ea-f5d6bb4654c8" />

And it's all for today:)
