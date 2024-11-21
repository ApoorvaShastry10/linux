Assignment 2

1. For each member in your team, provide 1 paragraph detailing what parts of the lab that member
implemented / researched. (You may skip this question if you are doing the lab by yourself).

Completed this assignment by myself

2. Describe in detail the steps you used to complete the assignment. Consider your reader to be someone
skilled in software development but otherwise unfamiliar with the assignment. Good answers to this
question will be recipes that someone can follow to reproduce your development steps.


Steps:
1. Fork the linux git repository (Repo - https://github.com/torvalds/linux )

2. Connect to the outer-vm - gcloud compute ssh outer-vm

3. Clone the forked linux git repository inside the outer-vm:
git clone https://github.com/ApoorvaShastry10/linux.git

4. Go into the linux directory by cd command:
	cd linux

5.  Install necessary kernel packages:
sudo apt-get install build-essential libncurses-dev flex bison libssl-dev libelf-dev zstd

6. Configuring linux kernel build:
	sudo make menuconfig

7. Building the kernel without installing it yet:
	sudo make -j$(nproc)
	sudo make modules
	sudo make modules_install

8. Taking the snapshot: in the left nav bar in the snapshot section, a snapshot is created by choosing the appropriate
disk from the option for which a snapshot has to be created.

9. Install the kernel which was built in step 7 and build initramfs:
	sudo make install
	mkinitramfs -o /boot/initrd.img-$(uname -r)

10. Reboot the outer-vm:
	sudo reboot

11. Edit the /arch/x86/kvm/vmx/vmx.c file 

12. After making the necessary changes kernel needs to be re-built and installed:
	sudo make -j$(nproc)
	sudo make modules
	sudo make modules_install
	sudo make install

13. Reboot the outer-vm
	sudo reboot

14. Check the latest version after rebuilding the kernel
	uname -r

15. Boot the inner-vm in a separate tab or in a screen:
	screen -S s1
      If inner-vm is created using virt-install, it can booted just by starting it
	sudo virsh start inner-vm
	sudo virsh console inner-vm

16. To check the print statements in outer-vm:
	sudo dmesg


3. Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there
more exits performed during certain VM operations? Approximately how many exits does a full VM
boot entail?

There is a steady accumulation of exits over the time of VM boot. The frequency of the number of exits is
not increasing at a stable rate. In my case, the cumulative count of exits ranges from 1.5 million to 2 million
during a boot sequence.



4. Of the exit types, which are the most frequent? Least?

In my case, exit type 10(CPIID),  exit type 1(handle_external_interupt), exit type 30 and few others are frequent.
Exit type 0(handle_expception_nmi), exit type 31, exit type 29, exit type 46 etc are least. Below attached is the
screenshot of the sudo dmesg command.


