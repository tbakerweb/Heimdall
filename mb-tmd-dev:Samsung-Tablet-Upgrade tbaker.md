mb-tmd-dev:Samsung-Tablet-Upgrade tbaker$ rm META-INF/
rm: META-INF/: is a directory
mb-tmd-dev:Samsung-Tablet-Upgrade tbaker$ rm -rf META-INF/
mb-tmd-dev:Samsung-Tablet-Upgrade tbaker$ rm -rf install system
mb-tmd-dev:Samsung-Tablet-Upgrade tbaker$ unzip lineage-14.1-20210423-UNOFFICIAL-klimtlte.zip -d .
Archive:  lineage-14.1-20210423-UNOFFICIAL-klimtlte.zip
signed by SignApk
replace ./system.patch.dat? [y]es, [n]o, [A]ll, [N]one, [r]ename: n
  inflating: ./META-INF/com/android/metadata
  inflating: ./META-INF/com/google/android/update-binary
  inflating: ./META-INF/com/google/android/updater-script
  inflating: ./META-INF/org/lineageos/releasekey
replace ./boot.img? [y]es, [n]o, [A]ll, [N]one, [r]ename: n
replace ./file_contexts.bin? [y]es, [n]o, [A]ll, [N]one, [r]ename: n
  inflating: ./install/bin/backuptool.functions
  inflating: ./install/bin/backuptool.sh
  inflating: ./install/bin/otasigcheck.sh
replace ./system.new.dat? [y]es, [n]o, [A]ll, [N]one, [r]ename: n
replace ./system.transfer.list? [y]es, [n]o, [A]ll, [N]one, [r]ename: n
  inflating: ./system/build.prop
  inflating: ./META-INF/com/android/otacert
  inflating: ./META-INF/MANIFEST.MF
  inflating: ./META-INF/CERT.SF
  inflating: ./META-INF/CERT.RSA
mb-tmd-dev:Samsung-Tablet-Upgrade tbaker$ n

rm -f system.patch.dat boot.img file_contexts.bin system.new.dat system.transfer.list

if [ -d "$HOME/SOURCE/toastedCoder/Samsung-Tablet-Upgrade-COPYFROMWIN/Samsung-Tablet-Upgrade/platform-tools-mac" ] ; then
 export PATH="$HOME/SOURCE/toastedCoder/Samsung-Tablet-Upgrade-COPYFROMWIN/Samsung-Tablet-Upgrade/platform-tools-mac:$PATH"
fi

-DCMAKE_PREFIX_PATH=/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core/Aliases/qt5

## Install Heimdall
git clone git@gitlab.com:BenjaminDobell/Heimdall.git
cd Heimdall
wget https://gitlab.com/BenjaminDobell/Heimdall/-/merge_requests/468.diff
git apply 468.diff

mkdir build
cd build
cmake -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Release -DQt5Widgets_DIR=/usr/local/opt/qt5/lib/cmake/Qt5Widgets ..
make
sudo cp bin/heimdall /usr/local/bin
sudo cp -r bin/heimdall-frontend.app /Applications

## Install INDI
cmake -DCMAKE_INSTALL_PREFIX=$HOME/opt -DCMAKE_BUILD_TYPE=Debug /Users/tbaker/SOURCE/_ref/indi-1.9.0 ..
make -j4
sudo make install
$ cmake . -DCMAKE_PREFIX_PATH=/usr/local/Cellar/qt5/5.3.2

## Fixing missing Qt5 stuff
brew install qt5
ls /usr/local/opt/qt5/lib/cmake/Qt5Widgets/Qt5WidgetsConfig.cmake
/usr/local/opt/qt5/lib/cmake/Qt5Widgets/Qt5WidgetsConfig.cmake
export CMAKE_PREFIX_PATH=/usr/local/opt/qt5/
cd ./build
cmake ../CMakeLists.txt
make -j8

## Flashing recovery with Heimdall
./heimdall flash --RECOVERY twrp-3.5.2_9-0-klimtlte.img --no-reboot --pit samsung-tablet.pit

## My current bootloader/recovery
Android system recovery <3e>
KOT49H.T707AUCU1ANH9

adb side loading fails with
E: failed to verify whole-file signature
E: signature verification failed
