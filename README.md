# mpy-esp32
 Micropython & ESP32 with MPY


## Install ESP-IDF
```
git clone -b v4.4.2 --recursive https://github.com/espressif/esp-idf.git
cd esp-idf
git submodule update --init --recursive
./install.sh
. ./export.sh
source export.sh
```

## Install MPY-Cross
```
cd ~
git clone https://github.com/micropython/micropython.git
cd micropython
make -C mpy-cross
cd ports/esp32
make submodules
make
```

## Permissions
```
sudo chown user /dev/ttyUSB0
```

## Convert .py to .mpy
```
mpy-cross file.py
```

## Flash firmware to ESP32
```
make erase
make deploy
```

## Flash python code to ESP32
```
cd micropython/ports/esp32/boards
mkdir own-python
cp -r GENERIC own-python
cp -r *.mpy # COPY FILES TO own-python DIRECTORY
####
make BOARD=own-python
idf.py -D MICROPY-BOARD=own-python build
idf.py flash
```