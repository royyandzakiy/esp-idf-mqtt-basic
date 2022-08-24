# ESP IDF MQTT - Basic

This is a basic implementation of the [MQTT example from esp idf SDK](https://github.com/espressif/esp-idf/tree/ae256e9ca23a85e05f6a9ff31805028d3e823f4d/examples/protocols/mqtt/tcp) with some changes to make it work for ESP IDF `release/v4.4.1`.

## IMPORTANT: 
I use ESP IDF in **release/v4.4.1**, other versions may or may not work accordingly

## Getting Started
- prepare your ESP IDF, make sure it uses the version `release/v4.4.1` or any other releases that would comply
- clone this repo `git clone https://github.com/royyandzakiy/esp-idf-mqtt-basic`
- start the idf configuration
    - if you use the ESP IDF extension in VSCode, just click on the gear icon
    - if you use cli, do `idf.py menuconfig` (i will assume, you have gotten idf.py working with the `{IDF PATH}/export.sh`)
- change these parameters:
    - WiFi SSID
    - WiFi Password (keep empty if there is none)
    - MQTT Broker URL
    - MQTT Broker Username (keep empty if there is none)
    - MQTT Broker Password (keep empty if there is none)
- Build, Flash, Monitor
- Check/subscribe your broker for the topic `/topic/qos1`, there should be a message `data_3` sent by the device
- You can test if the mqtt of the device is working by publishing to the topic `/topic/qos0`, and checking the serial monitor
- enjoy!

## To do:
- change the wifi implementation to then use the [ESP IDF WIFI Station repo](https://github.com/espressif/esp-idf/tree/ae256e9ca23a85e05f6a9ff31805028d3e823f4d/examples/wifi/getting_started/station)
    - as mentioned in the original [ESP IDF protocols repo](https://github.com/espressif/esp-idf/tree/ae256e9ca23a85e05f6a9ff31805028d3e823f4d/examples/protocols), to make an internet connection, this uses the function `example_connect()` which is currently unsafe and is used for simplification purposes (for details, go check the repo)
- change this repo into a component or submodule for ease of use. optionally make it into a cpp class/module

---

## Changes
I made some changes, because incompatibility of usage of the `esp_mqtt_client_config_t` from the original example (i think it uses a different esp idf version, haven't tracked which version it implements though). Adding these changes will make it work, following guidance from the [docs of release/v4.4](https://docs.espressif.com/projects/esp-idf/en/release-v4.4/esp32/api-reference/protocols/mqtt.html)
```
    esp_mqtt_client_config_t mqtt_cfg = {
        .host = CONFIG_BROKER_URL,
        .port = 1883,
        .username = CONFIG_BROKER_USERNAME,
        .password = CONFIG_BROKER_PASSWORD,
    };

```

I also added some config parameters for `BROKER_USERNAME` and `BROKER_PASSWORD`
```
config BROKER_USERNAME
        string "Broker Username"
        default ""
        help
            URL of the broker to connect to

    config BROKER_PASSWORD
        string "Broker Password"
        default ""
        help
            URL of the broker to connect to
```