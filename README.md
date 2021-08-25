# indi-weather-mqtt
INDI driver for weather monitoring from an arbitrary MQTT source.
This driver is superior to any existing driver as it can be fed
with data from virtually any source through local or public MQTT broker.
If your weather station can publish to MQTT topics, you can use 
it right away by subscribing to these topics. You can also
parse any weather date source with middleware (eg. node-red), publish
it to a MQTT broker and subscribe to it with the driver.

# Building
This assumes you already have INDI installed.

First, let's install some build tools, if you haven't already.
```
sudo apt install build-essential cmake
```

You must install the INDI ans Mosquitto development libraries.
```
sudo apt install libindi-dev libmosquitto1 libmosquitto-dev
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
Start your INDI server with indi-weather-mqtt by running
```
indiserver -v indi-weather-mqtt
```
Now you can monitor and control weather from a MQTT source of your choice!
