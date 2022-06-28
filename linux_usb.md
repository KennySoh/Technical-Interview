## Debugging USB 
```
lsusb // this show a list of connected usb, connect & disconnect to figure what has been connected
>> Bus 001 , Device 013 , ID 1d56:0032 Brother industries

lsusb -s 001:013 // finding specific info with Bus & Device

lsusb -sv 001:013 // verbose info



```
