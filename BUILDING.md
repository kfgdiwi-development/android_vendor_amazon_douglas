### Building

The build process is quite long and requires fair knowledge of Linux and its command line.

#### 1. Install Google's repo tool

```bash
# Add binary folder
mkdir -p ~/bin
# Add folder to path
PATH=~/bin:$PATH
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
source ~/.profile
```
#### 2. Download the Lineage OS 14.1 source code

```bash
# Create the source directory and cd to it
mkdir -p ~/android/lineage-14.1
cd <source-folder>
# Initialize the repo init
repo init -u git://github.com/LineageOS/android.git -b cm-14.1
# This will take a bit depending of your internet connection
repo sync
```

#### 3. Clone douglas proprietary repositories
```bash
# Vendor Tree
git clone https://github.com/douglas-development/android_vendor_amazon_douglas.git -b cm-14.1 vendor/amazon/douglas
# Device Tree
git clone https://github.com/douglas-development/android_device_amazon_douglas.git -b cm-14.1 device/amazon/douglas
# Kernel Tree
git clone https://github.com/douglas-development/android_kernel_amazon_douglas -b cm-14.1 kernel/amazon/douglas
```

#### 4. Start the build
```bash
# Source the envsetup
source ./build/envsetup.sh
# Lunch the device. You can use (eng, user, userdebug)
lunch cm_douglas-userdebug 
# Make bacon!
mka bacon -j$(nproc --all)
```

If all went correctly, you should locate your ROM.zip at ``out/target/product/douglas/lineage-XX.X-douglas-XXXXXXXX.zip``

