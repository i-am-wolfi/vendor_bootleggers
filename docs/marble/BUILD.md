# Bootleggers 16 (marble) - bring-up recipe
repo init -u https://github.com/LineageOS/android.git -b lineage-23.2 --git-lfs --depth=1
repo sync -c -j4 --force-sync --no-clone-bundle --no-tags --optimized-fetch --prune
git clone https://github.com/TheMuppets/proprietary_vendor_xiaomi_marble.git -b lineage-23.2 vendor/xiaomi/marble
git clone https://github.com/TheMuppets/proprietary_vendor_xiaomi_sm8450-common.git -b lineage-23.2 vendor/xiaomi/sm8450-common
# local_manifests/bootleggers.xml -> i-am-wolfi/vendor_bootleggers#sixteen em vendor/bootleggers
# device: bootleggers_marble.mk + AndroidProducts.mk (pasta docs/marble, forkar device depois)
source build/envsetup.sh
lunch bootleggers_marble-bp4a-userdebug   # ou -eng p/ debug
export USE_CCACHE=1 CCACHE_DIR=~/ccache; ccache -M 100G
LINEAGE_BUILD=marble mka bacon -j$(nproc --all)
