# openbsd-gcc-4.2.1-segfault
GCC 4.2.1 bug report

GCC segfault when compiling mlton-compile.100.c (one of many autogenerated MLton compiler bootstrap files)

```
$ gcc -std=gnu99 -c -O1 -w -m64 -I../build/lib/targets/self/include/ -I../build/lib/include/ -I/usr/local/include -fPIC -fno-common -fno-strict-aliasing -fomit-frame-pointer -o mlton-compile.100.o mlton-compile.100.c
```

Error output:
```
mlton-compile.100.c: In function 'Chunk100':
mlton-compile.100.c:176: internal compiler error: Segmentation fault
Please submit a full bug report,
with preprocessed source if appropriate.
See <URL:http://gcc.gnu.org/bugs.html> for instructions.
*** Error 1 in /usr/ports/pobj/mlton-8952ed443fab86d78d151b23f133c0ecacc95fc0/mlton-8952ed443fab86d78d151b23f133c0ecacc95fc0/bootstrap (Makefile:60 'mlton-compile.100.o')
*** Error 1 in . (Makefile:44 'do-build')
*** Error 1 in . (/usr/ports/infrastructure/mk/bsd.port.mk:2769 '/usr/ports/pobj/mlton-8952ed443fab86d78d151b23f133c0ecacc95fc0/.build_done')
*** Error 1 in /usr/ports/lang/mlton (/usr/ports/infrastructure/mk/bsd.port.mk:2495 'build')
```

System information:
```
# uname -a
OpenBSD www.my.domain 5.9 GENERIC#1761 amd64
```

```
# dmesg
OpenBSD 5.9 (GENERIC) #1761: Fri Feb 26 01:15:04 MST 2016
    deraadt@amd64.openbsd.org:/usr/src/sys/arch/amd64/compile/GENERIC
real mem = 2130575360 (2031MB)
avail mem = 2061905920 (1966MB)
mpath0 at root
scsibus0 at mpath0: 256 targets
mainbus0 at root
bios0 at mainbus0: SMBIOS rev. 2.8 @ 0xf6300 (9 entries)
bios0: vendor SeaBIOS version "rel-1.8.2-0-g33fbe13 by qemu-project.org" date 04/01/2014
bios0: QEMU Standard PC (i440FX + PIIX, 1996)
acpi0 at bios0: rev 0
acpi0: sleep states S3 S4 S5
acpi0: tables DSDT FACP SSDT APIC HPET
acpi0: wakeup devices
acpitimer0 at acpi0: 3579545 Hz, 24 bits
acpimadt0 at acpi0 addr 0xfee00000: PC-AT compat
cpu0 at mainbus0: apid 0 (boot processor)
cpu0: Virtual CPU 714389bda930, 2400.35 MHz
cpu0: FPU,VME,DE,PSE,TSC,MSR,PAE,MCE,CX8,APIC,SEP,MTRR,PGE,MCA,CMOV,PAT,PSE36,CFLUSH,MMX,FXSR,SSE,SSE2,HTT,SSE3,PCLMUL,SSSE3,FMA3,CX16,PCID,SSE4.1,SSE4.2,x2APIC,MOVBE,POPCNT,DEADLINE,AES,XSAVE
,AVX,F16C,RDRAND,HV,NXE,LONG,LAHF,ABM,FSGSBASE,BMI1,AVX2,SMEP,BMI2,ERMS,INVPCID,ARAT
cpu0: 64KB 64b/line 2-way I-cache, 64KB 64b/line 2-way D-cache, 512KB 64b/line 16-way L2 cache
cpu0: ITLB 255 4KB entries direct-mapped, 255 4MB entries direct-mapped
cpu0: DTLB 255 4KB entries direct-mapped, 255 4MB entries direct-mapped
cpu0: smt 0, core 0, package 0
mtrr: Pentium Pro MTRR support, 8 var ranges, 88 fixed ranges
cpu0: apic clock running at 1000MHz
cpu at mainbus0: not configured
ioapic0 at mainbus0: apid 0 pa 0xfec00000, version 11, 24 pins
acpihpet0 at acpi0: 100000000 Hz
acpiprt0 at acpi0: bus 0 (PCI0)
acpicpu0 at acpi0: C1(@1 halt!)
pvbus0 at mainbus0: KVM
pci0 at mainbus0 bus 0
pchb0 at pci0 dev 0 function 0 "Intel 82441FX" rev 0x02
pcib0 at pci0 dev 1 function 0 "Intel 82371SB ISA" rev 0x00
pciide0 at pci0 dev 1 function 1 "Intel 82371SB IDE" rev 0x00: DMA, channel 0 wired to compatibility, channel 1 wired to compatibility
pciide0: channel 0 disabled (no drives)
atapiscsi0 at pciide0 channel 1 drive 0
scsibus1 at atapiscsi0: 2 targets
cd0 at scsibus1 targ 0 lun 0: <QEMU, QEMU DVD-ROM, 2.5+> ATAPI 5/cdrom removable
cd0(pciide0:1:0): using PIO mode 4, DMA mode 2
uhci0 at pci0 dev 1 function 2 "Intel 82371SB USB" rev 0x01: apic 0 int 11
piixpm0 at pci0 dev 1 function 3 "Intel 82371AB Power" rev 0x03: apic 0 int 9
iic0 at piixpm0
vga1 at pci0 dev 2 function 0 "Cirrus Logic CL-GD5446" rev 0x00
wsdisplay0 at vga1 mux 1: console (80x25, vt100 emulation)
wsdisplay0: screen 1-5 added (80x25, vt100 emulation)
virtio0 at pci0 dev 3 function 0 "Qumranet Virtio Network" rev 0x00
vio0 at virtio0: address 56:00:00:27:4a:f5
virtio0: apic 0 int 11
virtio1 at pci0 dev 4 function 0 "Qumranet Virtio Storage" rev 0x00
vioblk0 at virtio1
scsibus2 at vioblk0: 2 targets
sd0 at scsibus2 targ 0 lun 0: <VirtIO, Block Device, > SCSI3 0/direct fixed
sd0: 46080MB, 512 bytes/sector, 94371840 sectors
virtio1: apic 0 int 11
virtio2 at pci0 dev 5 function 0 "Qumranet Virtio Memory" rev 0x00
viomb0 at virtio2
virtio2: apic 0 int 10
virtio3 at pci0 dev 6 function 0 "Qumranet Virtio RNG" rev 0x00
viornd0 at virtio3
virtio3: apic 0 int 10
isa0 at pcib0
isadma0 at isa0
fdc0 at isa0 port 0x3f0/6 irq 6 drq 2
fd0 at fdc0 drive 1: density unknown
pckbc0 at isa0 port 0x60/5 irq 1 irq 12
pckbd0 at pckbc0 (kbd slot)
wskbd0 at pckbd0: console keyboard, using wsdisplay0
pms0 at pckbc0 (aux slot)
wsmouse0 at pms0 mux 0
pcppi0 at isa0 port 0x61
spkr0 at pcppi0
usb0 at uhci0: USB revision 1.0
uhub0 at usb0 "Intel UHCI root hub" rev 1.00/1.00 addr 1
nvram: invalid checksum
uhidev0 at uhub0 port 1 configuration 1 interface 0 "QEMU QEMU USB Tablet" rev 2.00/0.00 addr 2
uhidev0: iclass 3/0
ums0 at uhidev0: 3 buttons, Z dir
wsmouse1 at ums0 mux 0
vscsi0 at root
scsibus3 at vscsi0: 256 targets
softraid0 at root
scsibus4 at softraid0: 256 targets
sd1 at scsibus4 targ 1 lun 0: <OPENBSD, SR CRYPTO, 005> SCSI2 0/direct fixed
sd1: 15358MB, 512 bytes/sector, 31454678 sectors
root on sd1a (7ff6fcc5f67bcc4a.a) swap on sd1b dump on sd1b
clock: unknown CMOS layout
```
