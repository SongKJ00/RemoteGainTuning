# RemoteGainTuning
GUI for Remote Gain Tuning with Zigbee(for Drone)

If you download the .exe file, you can tune gain value of your own drone with zigbee.

For use this program, you should connect zigbee module with USB to TTL, and connect that to computer USB port.

## Packet Structure

If you click the 'TRANSMIT' Button, the packet will be transmitted.

The packet structure is listed as below;

| Head 1 | Head 2 | Type | Payload | Tail | Checksum |
|:------:|:------:|:----------:|:----------:|:----:|:----------:|
| 0x53 | 0x4D | See belows | See belows | 0x50 | See belows |

* Head 1, Head 2

  Head 1, Head 2 are start bytes and fixed. 

* Type

  Type is explained that which gain will be changed.
  
  | Type | Contents |
  |:----:|:------------:|
  | 0x41 | Roll P Gain |
  | 0x42 | Roll I Gain |
  | 0x43 | Roll D Gain |
  | 0x44 | Pitch P Gain |
  | 0x45 | Pitch I Gain |
  | 0x46 | Pitch D Gain |
  | 0x47 | Yaw P Gain |
  | 0x48 | Yaw I Gain |
  | 0x49 | Yaw D Gain |
  
  
* Payload<br>
  Payload consists of 4 bytes(uint8_t).
  
  You will put gain value in textbox with float type, it will be changed to 4 bytes with uint8_t type by using Union(I used ctypes module).
  
* Tail

  Tail is just end byte and fixed with 0x50.
  
* Checksum

    Checksum is for checking packet integrity.<br>
   When you click the 'TRANSMIT' button, this program will calculate checksum automatically.<br>
    At recevier side, add all byte of each packets including checksum and if its result's lower byte is 0x00 it means it has no problem and the packet was transmitted successfully.
