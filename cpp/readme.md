##### esp8266

https://m.aliexpress.com/wholesale/nodemcu-v3.html?searchType=mainSearch&keywords=nodemcu-v3&shadingAction=&channel=direct

##### Text editor

https://visualstudio.microsoft.com/vs/community/

##### Driver to esp8266

https://platformio.org/install/ide?install=vscode

reboot

---

# Quick start

http://docs.platformio.org/en/latest/quickstart.html

Icon alien - quick access - PIO Home - Open - New project - Board NodeMCU 1.0 ....

#### src/main.cpp

```cpp
#include <Arduino.h>

void setup() {
  Serial.begin(9600);
}

void loop() {
  Serial.print("loop!!!!!!!");
  delay(1000);
}
```

Icon alien - quick access - Miscellaneous - New terminal

```sh
platformio
platformio device list
# connect esp8266 to your computer
platformio device list
platformio run --target upload --upload-port COM6
# blue light flash when you writing in the esp8266
platformio device monitor
# you can read "loop!!!!!!!!" each seconde
```

# web server

https://github.com/esp8266/Arduino/blob/master/libraries/ESP8266WebServer/examples

#### src/main.cpp

```cpp
#include <ESP8266WiFi.h>
#include <WiFiClient.h>
#include <ESP8266WebServer.h>
#include "index.h"

ESP8266WebServer server(80);

void handleRoot() {
  server.send(200, "text/html", mainPage);
}

void setup(void) {
  Serial.begin(9600);
  WiFi.mode(WIFI_STA);
  WiFi.begin("YOUR_SSID", "YOUR_PASSWORD");
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  server.on("/", handleRoot);
  server.begin();
  Serial.print("IP address: ");
  Serial.println(WiFi.localIP());
}

void loop(void) {
  server.handleClient();
}
```

#### src/index.h

```cpp
const char *mainPage = R""""(
<!DOCTYPE html>
<html lang="en">
<head>
  <title>ESP8266</title>
</head>
<body>

<div class="container">
  <h2>THIS WORK</h2>
</div>

</body>
</html>
)"""";
```

# add others libraries

Icon alien - quick access - PIO Home - Open - Libraries

- make empty search for most popular libraries
