# build_karnak

# Instructions to build LineageOS for karnak:

## Step 1: Setup the environment.

```sudo apt install -y bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev python-is-python3```

```mkdir -p ~/bin```

```mkdir -p ~/android/lineage```

```curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo```

```chmod a+x ~/bin/repo```

```git config --global user.email "you@example.com"```

```git config --global user.name "Your Name"```

```cd ~/android/lineage```

```repo init -u https://github.com/LineageOS/android.git -b lineage-18.1 -g default,-darwin```

## Step 2: Get the device manifest file.

https://github.com/srccrow/karnak_manifests

https://github.com/srccrow/karnak_manifests/blob/main/karnak_manifest.xml

https://github.com/srccrow/karnak_manifests/blob/main/linaro_manifest.xml

save them to: ```~/android/lineage/.repo/local_manifests```

then do: ```repo sync --jobs=32```

**Fix the kernel:**

```sed -i 's/const const struct/const struct/g' kernel/amazon/karnak/drivers/pinctrl/mediatek/pinctrl-mtk-common.h```

```sed -i 's/CONFIG_FRAME_WARN=1500/CONFIG_FRAME_WARN=1520/g' kernel/amazon/karnak/arch/arm64/configs/lineageos_karnak_defconfig```

```sed -i 's/CONFIG_FRAME_WARN,COMMON,,,1500,1500,1500,1500,1500,1500/CONFIG_FRAME_WARN,COMMON,,,1520,1520,1520,1520,1520,1520/g' kernel/amazon/karnak/scripts/kcrs/correct_config.csv```

## Step 3: Turn on caching to speed up build. Note that I used 300Gb instead of 100Gb (just personal preference).

```mkdir ~/ccache```

```export CCACHE_DIR=~/ccache```

```export USE_CCACHE=1```

```export CCACHE_EXEC=/usr/bin/ccache```

```ccache -M 300G```

```export ANDROID_JACK_VM_ARGS="-Dfile.encoding=UTF-8 -XX:+TieredCompilation -Xmx4G"```

## Step 4: Select Build.

```source build/envsetup.sh```

```rm -rf out/target/product/karnak/obj/KERNEL_OBJ/.version```

```rm -rf out/target/product/karnak/obj/KERNEL_OBJ/.config.old```

```lunch lineage_karnak-userdebug```

## Step 5: Build it!

```cmka```

```brunch karnak```

## Step 6: Replace boot.img

Replace boot.img inside the rom.zip, 

the SHA256 for the correct boot.img that allows to boot the OS is the following:

``SHA256: dbd503c5b6b8fd3652b93d5bc75ff666ac667607fe0f3cca7773e93b04d57c2f``

# Credits:

https://forum.xda-developers.com/t/rom-unstable-unlocked-karnak-lineage-18-1-25-october-2021.4352241

https://gitlab.com/mt8163/karnak_releases
