# EASYHOME-RCT-DS1
provide the rc-switch code for this rf 433 MHZ remote

Within my smart home project I came across to remote control my remote controlled switches.

The remote is of type EASYHOME RCT DS1 CR-A
---
MASTER ON
```
Decimal: 3556466 (24Bit) Binary: 001101100100010001110010 Tri-State: not applicable PulseLength: 100 microseconds Protocol: 3
Raw data: 7147,418,1105,408,1109,901,639,869,635,371,1109,902,654,854,626,382,1117,390,1094,915,640,367,1114,394,1117,391,1103,907,649,355,1116,392,1113,398,1107,902,640,867,632,875,638,369,1125,382,1112,898,626,380,1116,
```
---
MASTER OFF
```
Decimal: 3151714 (24Bit) Binary: 001100000001011101100010 Tri-State: not applicable PulseLength: 100 microseconds Protocol: 3
Raw data: 7138,424,1108,396,1108,904,631,876,620,386,1109,397,1110,399,1111,399,1117,390,1099,409,1105,405,1116,893,624,381,1103,909,627,881,626,877,653,357,1107,901,630,879,633,374,1116,392,1102,407,1103,904,631,377,1114,
```
---
Button A ON
```
Decimal: 3649372 (24Bit) Binary: 001101111010111101011100 Tri-State: not applicable PulseLength: 511 microseconds Protocol: 5
Raw data: 7158,487,21,5,17,16,960,427,1077,357,1134,875,651,861,654,848,644,868,664,346,1136,874,665,337,1117,892,659,844,660,853,647,860,646,364,1129,877,646,365,1129,876,655,857,651,858,642,366,1127,378,1126,

```
---
Button A OFF
```
Decimal: 3556476 (24Bit) Binary: 001101100100010001111100 Tri-State: not applicable PulseLength: 508 microseconds Protocol: 5
Raw data: 7108,616,879,432,1077,896,623,879,651,360,1128,874,646,855,652,353,1127,391,1084,962,559,451,1051,448,1038,473,1054,934,562,449,1055,458,1037,463,1040,951,570,925,586,928,574,916,586,926,615,361,1092,415,1120,

```

---
This is the code to read using rc-switch library
```
/*
  Example for receiving
  
  https://github.com/sui77/rc-switch/
  
  If you want to visualize a telegram copy the raw data and 
  paste it into http://test.sui.li/oszi/
*/

#include <RCSwitch.h>

RCSwitch mySwitch = RCSwitch();

void setup() {
  Serial.begin(115200);
  mySwitch.enableReceive(digitalPinToInterrupt(5));  // Receiver on interrupt 0 => that is pin #2
  Serial.print("booted");
}

void loop() {
  if (mySwitch.available()) {
    output(mySwitch.getReceivedValue(), mySwitch.getReceivedBitlength(), mySwitch.getReceivedDelay(), mySwitch.getReceivedRawdata(),mySwitch.getReceivedProtocol());
    mySwitch.resetAvailable();
  }
}
```
