# mesh-pixel
Open source hardware/software for inconspicuous, wireless ir-mesh led pixels

## ⚠️ Note ⚠️
**Please understand this is still in EARLY and UNPRIORITIZED development!!**


## 💡 The Idea
- Single-pixel leds with independent addresses and an (APRS-like?) IR propagation/retransmission scheme utilizing tv-remote-style IR transmissions (which will work well at night)
- Tiny PCBs with black solder mask, easy to attach harmlessly to trees and structures
- Central control via a master station with an esp32, authenticated WiFi AP with web app and lightweight API
- Super low power consumption (power by button cell)
- Low-cost components, easy to assemble and deploy


## Component Candidates
### Microcontroller
### IR Receiver
### IR Transmitter
### Pixel LED
### Battery

## IR Communication Scheme
The following information will be encoded into each packet
- 2 bit propagation control
    - broadcast (all retx once, no path/delay)
    - request (retransmit according to path and delay)
    - response (do not retransmit same-id request but honor path and delay)
- 6 bit rolling message id
- 1 byte .1s precision relative time of request origination or time sync time
- 12 bit sender and destination addr (3 bytes total) 
   Address of destination device, 2 bytes.
   Master is always 0x0000
   Packet is never retransmitted by this address
- path
    - 4 bit retx's so far
    - 4 bit retx's total
    (retransmit if total>so far)
- delay (1 byte)
    Minimum delay before retransmission   
    (used to reduce interference)
- command (1 byte)
    - sync time
    - panic (off then retx)
    - on
    - off
    - test
      (returns response with ACK, current relative time according to the device)
    - ACK
    - NAK
    - strobe
- Data byte
- 2 reserved bytes
- Checksum

12 bytes total...




