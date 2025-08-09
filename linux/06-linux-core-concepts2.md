# Linux Core Concepts 2
**Continue learning the core concepts of Linux** - 09/08/2025 - 15minutes

[LINK](https://studio.kodekloud.com/labs/linux/linux-core-concepts-2) - 09/08/2025 -

## Exercises

**Going forward, you would need to make use of `sudo` for running several commands.
In such cases, run `sudo` before the command**

**Example: `sudo ls /root`**
**Bob's password is `caaleston123`**

### What is the `init process` used by this system?
```
bob@caleston-lp10:~$ ps -p 1
    PID TTY          TIME CMD
      1 ?        00:00:00 systemd
bob@caleston-lp10:~$ 
```
The 1 that i put is the process ID, the first process always starts with 1

"Process ID 1 is usually the init process primarily responsible for starting and shutting down the system"

### What is the `defaut system target` set in this system?
```bash
bob@caleston-lp10:~$ systemctl get-default
graphical.target
bob@caleston-lp10:~$ 
```

### Now, change the target to multi-user.target
```bash
bob@caleston-lp10:~$ systemctl get-default
graphical.target
bob@caleston-lp10:~$ systemctl set-default multi-user.target
Failed to set default target: The name org.freedesktop.PolicyKit1 was not provided by any .service files
bob@caleston-lp10:~$ 
bob@caleston-lp10:~$ sudo su
root@caleston-lp10:/home/bob# systemctl set-default multi-user.target
Created symlink /etc/systemd/system/default.target → /lib/systemd/system/multi-user.target.
root@caleston-lp10:/home/bob# systemctl get-default
multi-user.target
root@caleston-lp10:/home/bob# 
```
### What type of file is `firefox.deb` located at `/home`?A
```bash
root@caleston-lp10:~# pwd
/root
root@caleston-lp10:~# ls
firefox.deb  sample_script.sh  script1  script2  script3
```
In this case -> `Debian binary package file`

### What type of file is `sample_script.sh` located at `/root`?
```bash
root@caleston-lp10:~# cat sample_script.sh 
#!/bin/bash
while true
do
        date
        sleep 100
done
root@caleston-lp10:~# 
```
In this case -> `Bash Shell Script`
### You are asked to install a new `third-party IDE (integrated development environment)` in the system.
**Which directory is the recommended choice for the installation?**

In this case:
```bash
/opt
```

### Which directory contains the files related to the block devices that can be seen when running the `lsblk` command?
```bash
root@caleston-lp10:~# lsblk
lsblk: /proc/swaps: parse error at line 1 -- ignored
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda       8:0    0   20G  0 disk 
|-sda1    8:1    0 19.9G  0 part /lib/modules/5.15.0-1083-gcp
|-sda14   8:14   0    4M  0 part 
`-sda15   8:15   0  106M  0 part 
nvme0n1 259:0    0  375G  0 disk 
nvme0n2 259:1    0  375G  0 disk 
nvme0n3 259:2    0  375G  0 disk 
nvme0n4 259:3    0  375G  0 disk 
root@caleston-lp10:~# 
```
In this case -> `/dev`

### What is the name of the `vendor` for the `Ethernet Controller` used in this system?
```bash
root@caleston-lp10:~# lshw
caleston-lp10               
    description: Computer
    width: 64 bits
    capabilities: smp vsyscall32
  *-core
       description: Motherboard
       physical id: 0
     *-memory
          description: System memory
          physical id: 0
          size: 62GiB
     *-cpu
          product: Intel(R) Xeon(R) CPU @ 2.80GHz
          vendor: Intel Corp.
          physical id: 1
          bus info: cpu@0
          width: 64 bits
          capabilities: fpu fpu_exception wp vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp x86-64 constant_tsc rep_good nopl xtopology nonstop_tsc cpuid tsc_known_freq pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch invpcid_single ssbd ibrs ibpb stibp ibrs_enhanced fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm avx512f avx512dq rdseed adx smap clflushopt clwb avx512cd avx512bw avx512vl xsaveopt xsavec xgetbv1 xsaves arat avx512_vnni md_clear arch_capabilities
     *-pci
          description: Host bridge
          product: 440FX - 82441FX PMC [Natoma]
          vendor: Intel Corporation
          physical id: 100
          bus info: pci@0000:00:00.0
          version: 02
          width: 32 bits
          clock: 33MHz
        *-isa
             description: ISA bridge
             product: 82371AB/EB/MB PIIX4 ISA
             vendor: Intel Corporation
             physical id: 1
             bus info: pci@0000:00:01.0
             version: 03
             width: 32 bits
             clock: 33MHz
             capabilities: isa bus_master
             configuration: latency=0
        *-bridge UNCLAIMED
             description: Bridge
             product: 82371AB/EB/MB PIIX4 ACPI
             vendor: Intel Corporation
             physical id: 1.3
             bus info: pci@0000:00:01.3
             version: 03
             width: 32 bits
             clock: 33MHz
             capabilities: bridge bus_master
             configuration: latency=0
        *-generic:0
             description: Non-VGA unclassified device
             product: Virtio SCSI
             vendor: Red Hat, Inc.
             physical id: 3
             bus info: pci@0000:00:03.0
             version: 00
             width: 32 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=virtio-pci latency=0
             resources: irq:11 ioport:c040(size=64) memory:c0102000-c010207f
           *-virtio0 UNCLAIMED
                description: Virtual I/O device
                physical id: 0
                bus info: virtio@0
                configuration: driver=virtio_scsi
        *-storage
             description: Non-Volatile memory controller
             product: Google, Inc.
             vendor: Google, Inc.
             physical id: 4
             bus info: pci@0000:00:04.0
             version: 01
             width: 64 bits
             clock: 33MHz
             capabilities: storage nvm_express bus_master cap_list
             configuration: driver=nvme latency=0
             resources: irq:11 memory:c0000000-c0003fff memory:c0101000-c01011ff
        *-network
             description: Ethernet controller
             product: Virtio network device
             vendor: Red Hat, Inc.
             physical id: 5
             bus info: pci@0000:00:05.0
             version: 00
             width: 32 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=virtio-pci latency=0
             resources: irq:10 ioport:c000(size=64) memory:c0100000-c01003ff
           *-virtio1 UNCLAIMED
                description: Virtual I/O device
                physical id: 0
                bus info: virtio@1
                configuration: driver=virtio_net
        *-generic:1
             description: Unclassified device
             product: Virtio RNG
             vendor: Red Hat, Inc.
             physical id: 6
             bus info: pci@0000:00:06.0
             version: 00
             width: 32 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=virtio-pci latency=0
             resources: irq:10 ioport:c080(size=32) memory:c0103000-c010303f
           *-virtio2 UNCLAIMED
                description: Virtual I/O device
                physical id: 0
                bus info: virtio@2
                configuration: driver=virtio_rng
  *-network:0
       description: Ethernet interface
       physical id: 1
       logical name: eth0
       serial: 02:42:ac:10:ee:bb
       size: 10Gbit/s
       capabilities: ethernet physical
       configuration: autonegotiation=off broadcast=yes driver=veth driverversion=1.0 duplex=full ip=172.16.238.187 link=yes multicast=yes port=twisted pair speed=10Gbit/s
  *-network:1
       description: Ethernet interface
       physical id: 2
       logical name: eth1
       serial: 02:42:ac:10:ef:bb
       size: 10Gbit/s
       capabilities: ethernet physical
       configuration: autonegotiation=off broadcast=yes driver=veth driverversion=1.0 duplex=full ip=172.16.239.187 link=yes multicast=yes port=twisted pair speed=10Gbit/s
  *-network:2
       description: Ethernet interface
       physical id: 3
       logical name: eth2
       serial: 02:42:ac:11:00:04
       size: 10Gbit/s
       capabilities: ethernet physical
       configuration: autonegotiation=off broadcast=yes driver=veth driverversion=1.0 duplex=full ip=172.17.0.4 link=yes multicast=yes port=twisted pair speed=10Gbit/s
root@caleston-lp10:~# lshw | grep Ethernet
             description: Ethernet controller
       description: Ethernet interface
       description: Ethernet interface
       description: Ethernet interface
root@caleston-lp10:~# lshw | grep Ethernet -A 10 -B 10
             vendor: Google, Inc.
             physical id: 4
             bus info: pci@0000:00:04.0
             version: 01
             width: 64 bits
             clock: 33MHz
             capabilities: storage nvm_express bus_master cap_list
             configuration: driver=nvme latency=0
             resources: irq:11 memory:c0000000-c0003fff memory:c0101000-c01011ff
        *-network
             description: Ethernet controller
             product: Virtio network device
             vendor: Red Hat, Inc.
             physical id: 5
             bus info: pci@0000:00:05.0
             version: 00
             width: 32 bits
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=virtio-pci latency=0
             resources: irq:10 ioport:c000(size=64) memory:c0100000-c01003ff
--
             clock: 33MHz
             capabilities: bus_master cap_list
             configuration: driver=virtio-pci latency=0
             resources: irq:10 ioport:c080(size=32) memory:c0103000-c010303f
           *-virtio2 UNCLAIMED
                description: Virtual I/O device
                physical id: 0
                bus info: virtio@2
                configuration: driver=virtio_rng
  *-network:0
       description: Ethernet interface
       physical id: 1
       logical name: eth0
       serial: 02:42:ac:10:ee:bb
       size: 10Gbit/s
       capabilities: ethernet physical
       configuration: autonegotiation=off broadcast=yes driver=veth driverversion=1.0 duplex=full ip=172.16.238.187 link=yes multicast=yes port=twisted pair speed=10Gbit/s
  *-network:1
       description: Ethernet interface
       physical id: 2
       logical name: eth1
       serial: 02:42:ac:10:ef:bb
       size: 10Gbit/s
       capabilities: ethernet physical
       configuration: autonegotiation=off broadcast=yes driver=veth driverversion=1.0 duplex=full ip=172.16.239.187 link=yes multicast=yes port=twisted pair speed=10Gbit/s
  *-network:2
       description: Ethernet interface
       physical id: 3
       logical name: eth2
       serial: 02:42:ac:11:00:04
       size: 10Gbit/s
       capabilities: ethernet physical
       configuration: autonegotiation=off broadcast=yes driver=veth driverversion=1.0 duplex=full ip=172.17.0.4 link=yes multicast=yes port=twisted pair speed=10Gbit/s
root@caleston-lp10:~# 
```

In this case -> `Red Hat, Inc.`
