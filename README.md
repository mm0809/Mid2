# mid2

## How to set up and run my program
1. Creat ```mbed_app.json```
``` json
{
    "config": {
    "wifi-ssid": {
            "help": "WiFi SSID",
            "value": "\"SSID\""
    },
    "wifi-password": {
            "help": "WiFi Password",
            "value": "\"PASSWORD\""
    }
    },
    "target_overrides": {
        "B_L4S5I_IOT01A": {
            "target.components_add": ["ism43362"],
            "ism43362.provide-default": true,
            "target.network-default-interface-type": "WIFI",
            "target.macros_add" : ["MBEDTLS_SHA1_C"]
        }
    }
}
```
2. Compile the program
```
$ sudo mbed compile --source . --source ~/ee2405/mbed-os/ -m B_L4S5I_IOT01A -t GCC_ARM --profile tflite.json -f
```
3. Wait for mbed initialize 
5. Execute ```$ sudo python3 wifi_mqtt/mqtt_client.py```

## explain
I use serial port to send data between PC and mbed.
我判斷的feature是 "加速度改變方向是否有超過90度"
所以我除了計算所有"測量加速度向量夾腳"與"參考加速度向量"的夾角外，還要使用外積去確認"測量加速度向量夾腳"在參考向量的哪一測。
因為有可能參考向量A 與兩個向量B,C夾角小於90度，而B C夾角卻大於90度。
