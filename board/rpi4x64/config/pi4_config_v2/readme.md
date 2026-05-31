this is config rasp pi 4 support:
+ wifi
+ ssh
+ dbus
+ glibc
+ rootfs-overlay
+ auto enable wifi ssh
+ update name wellcome

git buildroot
git clone https://github.com/buildroot/buildroot.git

# Guide
make raspberrypi4_64_defconfig
make menuconfig

SSH
Target packages
 └── Networking applications
      └── dropbear
           [*] dropbear

WIFI
Target packages
 └── Networking applications
      [*] iw
      [*] wpa_supplicant
            [*] Enable nl80211 support
            [*] Install wpa_cli binary
            [*] Install wpa_passphrase binary
            [*] Enable the Unix-socket control interface

KERNEL
DRIVER
make linux-menuconfig
Networking support
 └── Wireless
      <*> cfg80211
      <*> mac80211
Device Drivers
 └── Network device support
      └── Wireless LAN
           <M> Broadcom FullMAC WLAN driver
               [*] SDIO bus interface support

make -j$(nproc)

# config
LOAD MODULE
modprobe brcmfmac

vi /etc/wpa_supplicant.conf
    ctrl_interface=/var/run/wpa_supplicant
    country=VN
    update_config=1

    network={
        ssid="TEN_WIFI"
        psk="MAT_KHAU_WIFI"
        key_mgmt=WPA-PSK
    }

CONNECT WIFI
ip link set wlan0 up
wpa_supplicant -B -Dnl80211 -i wlan0 -c /etc/wpa_supplicant.conf

DHCP WLAN
udhcpc -i wlan0

# ssh
dropbear -R -E

SET PASS
passwd

# copy ssh file
scp test.txt root@192.168.1.123:/tmp/

# copy ssh folder
scp -r myfolder root@192.168.1.123:/root/

# copy ssh port other 22
scp -P 2222 file.txt root@192.168.1.123:/root/
scp -P <potrt> file.txt root@192.168.1.123:/root/

