# indi-weather-mqtt
INDI driver for weather monitoring from an arbitrary MQTT source

# Building
This assumes you already have INDI installed.

First, let's install some build tools, if you haven't already.
```
sudo apt install build-essential cmake
```

You must install the INDI ans Mosquitto development libraries.
```
sudo apt install libindi-dev libmosquitto-dev
```

Okay, we're ready to get the source and build it.
```
git clone https://github.com/rkaczorek/indi-weather-mqtt.git
cd indi-weather-mqtt
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=/usr ..
make
sudo make install
```

# Running
Start your INDI server
Start indi-weather-mqtt INDI driver

Now you can monitor and control weather from a MQTT source of your choice!
