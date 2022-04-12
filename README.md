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

```repo init -u https://github.com/LineageOS/android.git -b lineage-18.1```

## Step 2: Get the device manifest file.

https://github.com/srccrow/karnak_manifests

https://github.com/srccrow/karnak_manifests/blob/main/karnak.xml

save it to: ```~/android/lineage/.repo/local_manifests/karnak.xml```

then do: ```repo sync```
