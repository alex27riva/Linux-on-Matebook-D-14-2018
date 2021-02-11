# Linux Mint on Matebook D 14 2018

This is a short guide on how to correctly configure Linux Mint 20.1 Ulyssa on Matebook D 14 2018 (Ryzen 5 2500U).

## Update the kernel

After installation I raccomend you to install the latest 5.8 kernel available.

I currently run version `5.8.0-41-generic`

## Fixing boot warnings

During boot you get the following messages, you can also view them by running `sudo dmesg --level=err`

- AMD-Vi: [Firmware Bug]: : IOAPIC[4] not in IVRS table

- AMD-Vi: [Firmware Bug]: : IOAPIC[5] not in IVRS table

- AMD-Vi: [Firmware Bug]: : No southbridge IOAPIC found

- AMD-Vi: Disabling interrupt remapping

- AMD-Vi: Unable to read/write to IOMMU perf counter.

- snd_pci_acp3x 0000:02:00.5: Invalid ACP audio mode : 1

To fix some of these errors, just add the following string to /etc/default/grub file

`ivrs_ioapic[4]=00:14.0 ivrs_ioapic[5]=00:00.2`

Before making any changes is a good thing to backup the file, you can do that with the following commands:

1. `cd /etc/default/grub`

2. `cp grub grub.orig` (this command make a copy of the configuration file)

Then add the string above in `GRUB_CMDLINE_LINUX_DEFAULT` before `quiet splash` keyword.

The full line looks like this:

`GRUB_CMDLINE_LINUX_DEFAULT="ivrs_ioapic[4]=00:14.0 ivrs_ioapic[5]=00:00.2 quiet splash"`



After doing that, run `sudo update-grub` for the changes to take effect.

Reboot the system, now 4 warnings are fixed.
