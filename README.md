# ECC608-httpsconnection-ioprotection

This issues "GET" request to https server and get a responce with IO protection for ECDH premaster secret transmission, which is provided by ATECC608A capability.

# Requirements

  Platformio with VS Code environment.
  install "Espressif 32" platform definition on Platformio  
  Prior to compile this project, you must copy "cert_chain.c", which is made by privious step [ECC608-Provision](https://github.com/kmwebnet/ECC608-Provision) to "src" folder.  

  you need to modify the definition and variables in main.c as follows:  
  ```
// your SSID and PASS
#define EXAMPLE_WIFI_SSID ""
#define EXAMPLE_WIFI_PASS ""

// Trusted CA certificate for verifying HTTPS server
const unsigned char rootcacert[]={
"-----BEGIN CERTIFICATE-----\n"
"-----END CERTIFICATE-----\n"
};

// URL , port number which you want to connect
status = atca_connect("" , "", &cfg);

  ```


# Environment reference
  
  Espressif ESP32-DevkitC
  this project initialize both of I2C 0,1 port, and the device on I2C port 0 is absent.
  pin assined as below:


      I2C 0 SDA GPIO_NUM_18
      I2C 0 SCL GPIO_NUM_19

      I2C 1 SDA GPIO_NUM_21
      I2C 1 SCL GPIO_NUM_22
          
  Microchip ATECC608A(on I2C port 1)

# Usage

you need to change a serial port number which actually connected to ESP32 in platformio.ini.

# Run this project

At first, you need to create self-signed CA chain by using python scripts step-by-step in "scripts" folder for test purpose.  
the scripts will generate "cert_chain.c" and "provision.h" which is mandatory to compile main C source code.  
You need to place 2 of them in "src" folder and,then execute "Upload" on Platformio. 

# Result

If you run this project with success, you can find the results on serial console as follows:

```
HTTP/1.1 200 OK
Date: Thu, 13 Jun 2019 08:35:11 GMT
Server: Apache/2.4.39 (Unix) OpenSSL/1.1.1
Last-Modified: Mon, 11 Jun 2007 18:53:14 GMT
ETag: "2d-432a5e4a73a80"
Accept-Ranges: bytes
Content-Length: 45
Connection: close
Content-Type: text/html

<html><body><h1>It works!</h1></body></html>
```

# License

This software is released under the MIT License, see LICENSE.
