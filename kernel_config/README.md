Modified Arch Linux Kernel configuartion to enable hardware devices for the Chuwi Hi12 tablet.

Tested with kernel 4.12

The following have been tested and confirmed to work
Wirless
Touchscreen
Keyboard dock and mouse

To be tested
Audio
HDMI output
Audio over HDMI
Accelerometer
OTG
SD card slot

I will be doing more testing as I go along and will trim out more uneeded drivers.

Here is a list of system info from the Chuwi Hi12

Linux chuwi 4.12.0-rc3-retrop.co.uk+ #1 SMP PREEMPT Sun Jun 4 02:32:18 BST 2017 x86_64 GNU/Linux

lscpu
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                4
On-line CPU(s) list:   0-3
Thread(s) per core:    1
Core(s) per socket:    4
Socket(s):             1
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 76
Model name:            Intel(R) Atom(TM) x5-Z8350  CPU @ 1.44GHz
Stepping:              4
CPU MHz:               479.970
CPU max MHz:           1920.0000
CPU min MHz:           480.0000
BogoMIPS:              2881.00
Virtualization:        VT-x
L1d cache:             24K
L1i cache:             32K
L2 cache:              1024K
NUMA node0 CPU(s):     0-3
Flags:                 fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht 
tm pbe syscall nx rdtscp lm constant_tsc arch_perfmon pebs bts rep_good nopl xtopology tsc_reliable nonstop_tsc cpuid aperfmperf 
tsc_known_freq pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 cx16 xtpr pdcm sse4_1 sse4_2 movbe popcnt tsc_deadline_timer aes 
rdrand lahf_lm 3dnowprefetch epb tpr_shadow vnmi flexpriority ept vpid tsc_adjust smep erms dtherm ida arat

lsmod
Module                  Size  Used by
nls_iso8859_1          16384  1
nls_cp437              20480  1
vfat                   20480  1
fat                    65536  1 vfat
snd_hdmi_lpe_audio     24576  2
joydev                 20480  0
gpio_keys              20480  0
mousedev               20480  0
evdev                  24576  14
intel_rapl             20480  0
input_leds             16384  0
intel_powerclamp       16384  0
coretemp               16384  0
crct10dif_pclmul       16384  0
crc32_pclmul           16384  0
crc32c_intel           24576  0
ghash_clmulni_intel    16384  0
pcbc                   16384  0
aesni_intel           167936  0
aes_x86_64             20480  1 aesni_intel
crypto_simd            16384  1 aesni_intel
glue_helper            16384  1 aesni_intel
cryptd                 20480  3 crypto_simd,ghash_clmulni_intel,aesni_intel
intel_cstate           16384  0
wdat_wdt               16384  0
pcspkr                 16384  0
thermal                20480  0
goodix                 16384  0
snd_soc_rt5651         81920  0
battery                20480  0
snd_soc_rt5670        122880  0
snd_soc_rt5645        135168  0
snd_soc_rt5640        110592  0
snd_soc_rl6231         16384  4 snd_soc_rt5670,snd_soc_rt5640,snd_soc_rt5645,snd_soc_rt5651
i915                 1449984  40
intel_gtt              20480  1 i915
drm_kms_helper        126976  1 i915
snd_intel_sst_acpi     16384  0
snd_intel_sst_core     69632  1 snd_intel_sst_acpi
snd_soc_sst_atom_hifi2_platform    86016  1 snd_intel_sst_core
snd_soc_sst_match      16384  1 snd_intel_sst_acpi
intel_hid              16384  0
sparse_keymap          16384  1 intel_hid
snd_soc_core          192512  5 snd_soc_rt5670,snd_soc_rt5640,snd_soc_sst_atom_hifi2_platform,snd_soc_rt5645,snd_soc_rt5651
snd_compress           20480  1 snd_soc_core
snd_pcm_dmaengine      16384  1 snd_soc_core
snd_pcm                90112  9 
snd_soc_rt5670,snd_hdmi_lpe_audio,snd_pcm_dmaengine,snd_soc_rt5640,snd_soc_sst_atom_hifi2_platform,snd_soc_rt5645,snd_soc_core,snd_soc_rt5651
hci_uart               90112  0
r8723bs               589824  0
btbcm                  16384  1 hci_uart
btqca                  16384  1 hci_uart
extcon_intel_int3496    16384  0
btintel                16384  1 hci_uart
extcon_core            20480  1 extcon_intel_int3496
bluetooth             483328  4 hci_uart,btintel,btqca,btbcm
mei_txe                20480  0
drm                   286720  24 i915,drm_kms_helper
mei                    81920  1 mei_txe
cfg80211              524288  1 r8723bs
syscopyarea            16384  1 drm_kms_helper
snd_timer              28672  1 snd_pcm
snd                    65536  9 snd_compress,snd_hdmi_lpe_audio,snd_timer,snd_soc_sst_atom_hifi2_platform,snd_soc_core,snd_pcm
sysfillrect            16384  1 drm_kms_helper
sysimgblt              16384  1 drm_kms_helper
i2c_designware_platform    16384  0
i2c_designware_core    20480  1 i2c_designware_platform
fb_sys_fops            16384  1 drm_kms_helper
i2c_algo_bit           16384  1 i915
soundcore              16384  1 snd
ac97_bus               16384  1 snd_soc_core
processor_thermal_device    16384  0
intel_soc_dts_iosf     16384  1 processor_thermal_device
ecdh_generic           24576  1 bluetooth
lpc_ich                24576  0
rfkill                 20480  6 bluetooth,cfg80211
tpm_crb                16384  0
int3406_thermal        16384  0
tpm_tis                16384  0
video                  36864  2 int3406_thermal,i915
dptf_power             16384  0
tpm_tis_core           20480  1 tpm_tis
int3403_thermal        16384  0
int340x_thermal_zone    16384  2 int3403_thermal,processor_thermal_device
int3400_thermal        16384  0
acpi_thermal_rel       16384  1 int3400_thermal
8250_dw                16384  0
soc_button_array       16384  0
tpm                    49152  3 tpm_tis,tpm_crb,tpm_tis_core
acpi_pad               16384  0
button                 16384  1 i915
spi_pxa2xx_platform    24576  0
sch_fq_codel           20480  5
ip_tables              24576  0
x_tables               28672  1 ip_tables
ext4                  536576  1
crc16                  16384  2 bluetooth,ext4
jbd2                   90112  1 ext4
fscrypto               24576  1 ext4
mbcache                16384  1 ext4
sd_mod                 49152  3
hid_generic            16384  0
usbhid                 45056  0
hid                   110592  2 hid_generic,usbhid
uas                    24576  0
usb_storage            65536  3 uas
scsi_mod              155648  3 sd_mod,usb_storage,uas
mmc_block              36864  0
xhci_pci               16384  0
xhci_hcd              184320  1 xhci_pci
usbcore               208896  5 usbhid,usb_storage,xhci_pci,uas,xhci_hcd
usb_common             16384  1 usbcore
sdhci_acpi             16384  0
sdhci                  40960  1 sdhci_acpi
led_class              16384  2 sdhci,input_leds
mmc_core              122880  4 sdhci,mmc_block,sdhci_acpi,r8723bs


lspci
00:00.0 Host bridge: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series SoC Transaction Register (rev 36)
00:02.0 VGA compatible controller: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series PCI Configuration 
Registers (rev 36)
00:03.0 Multimedia controller: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series Imaging Unit (rev 36)
00:0b.0 Signal processing controller: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series Power Management 
Controller (rev 36)
00:14.0 USB controller: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series USB xHCI Controller (rev 36)
00:1a.0 Encryption controller: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series Trusted Execution Engine (rev 
36)
00:1f.0 ISA bridge: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series PCU (rev 36)


lsusb
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 258a:6a88  
Bus 001 Device 003: ID 05e3:0608 Genesys Logic, Inc. Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub


