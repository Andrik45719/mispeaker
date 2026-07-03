mkdir ~/mispeaker
chmod 0777 ~/mispeaker
cd ~/mispeaker

#copy Dokerfile to ~/mispeaker

docker build -t mispeaker_builder .

docker run -v ~/mispeaker:/home/user -it mispeaker_builder /bin/bash


git clone https://git.archive.openwrt.org/14.07/openwrt.git openwrt-14.07
cd openwrt-14.07

./scripts/feeds update -a
./scripts/feeds install -a

#copy openwrt-14.07_patch to openwrt-14.07
chmod -R 0777 ~/mispeaker

make menuconfig
  Target System ->Amlogic meson

  [*] Advanced configuration options
    [*] Toolchain Options
        C Library implementation (Use eglibc) 
          eglibc version (eglibc 2.19) 

  Libraries
      SSL
        [M] libopenssl
          Configuration
            [*] Enable elliptic curve support
              [*] Enable ec2m support
            [*] Crypto acceleration support
              [*] Digests acceleration support


make download
make

make package/libs/openssl/{clean,compile} V=sc
make package/network/utils/curl/compile V=s

./scripts/feeds install mpd-full
make package/feeds/packages/mpd/{clean,compile} V=s



##############################################

./staging_dir/toolchain-arm_cortex-a9+neon_gcc-4.8-linaro_eglibc-2.19_eabi/bin/arm-openwrt-linux-gnueabi-gcc test.c -o test

