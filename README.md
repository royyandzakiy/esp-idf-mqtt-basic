# ESP IDF MQTT - Basic

This is a basic implementation of the [MQTT example from esp idf SDK](https://github.com/espressif/esp-idf/tree/ae256e9ca23a85e05f6a9ff31805028d3e823f4d/examples/protocols/mqtt/tcp). 

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
    - MQTT Broker Username
    - MQTT Broker Password
- Build, Compile, Flash, Monitor
- Check you broker for the topic `/topic/qos1`, there should be a message `data_3`
- You can test the mqtt of the device by publishing to the topic `/topic/qos0`
- enjoy!

---

## Changes
I made some changes, because in implementation of the `esp_mqtt_client_config_t` from the original example. this way it will work.
```
    esp_mqtt_client_config_t mqtt_cfg = {
        .host = CONFIG_BROKER_URL,
        .port = 1883,
        .username = CONFIG_BROKER_USERNAME,
        .password = CONFIG_BROKER_PASSWORD,
    };

```

I also added a parameter for BROKER_USERNAME and BROKER_PASSWORD
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