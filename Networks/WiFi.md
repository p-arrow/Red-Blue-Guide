## WIFI Standards (802.11)

![grafik](https://user-images.githubusercontent.com/84674087/132377369-bd5976eb-bf94-4c42-8aaf-4519eaf1b197.png)

## WIFI Frequence Modes

#### DSSS (Direct-Sequence Spread Spectrum)
- Common for WiFi / 802.11b
- Non-Overlapping Channels for 2.4GHz (wasting frequency though)

#### FHSS (Frequency-Hopping Spread Spectrum)
- Increased security due to hopping
- Slower speed

#### OFDM (Orthogonal Frequency-Division Multiplexing)
- Common for WiFi / 802.11n
- Slow modulation & Simultaneous transmission over 52 data streams
- Higher data rate while lower inteference between data streams

**Best Practice**
- Use Channel 1, 6 and 11 --> prevent overlapping frequency in 2.4GHz band (802.11b/g/n)


## WIFI Service Sets (AccessPoint (AP) Placement)
1. Careful planning to prevent APs from interefering with one another
2. Maintain desired area coverage
3. Overlap by using different channels is acceptable
4. In 2.4GHz, cells should have 10-15% coverage overlap (honeycomb pattern) to avoid drop out
5. All clients of WAP are single collision domain (!)

![grafik](https://user-images.githubusercontent.com/84674087/132377632-ccfb4791-db78-464e-b381-c2a7e885998a.png)


## WIFI Security

#### CSMA/CA (Carrier Sense Multiple Access/Collision Avoidance)
- Proactive Method (!)
- WIFI uses CSMA/CA to control access to medium
- CSMA/CA listens for other TX before starting own TX

#### Pre-Shared Key (PSK)
- Scalability is difficult if key is compromised (!)
- All clients must know the same password (!)

#### WEP (Wired Equivalent Privacy)
- Static 40bit PSK
- Later upgraded to 64bit and 128bit
- Initialization Vector (IV) 24bit in clear text (BruteForce possible!)

#### WPA (Wireless Protected Access)
- TKIP (i/o IV) and MIC
- Symmetric Encryption RC4
- Uses PSK
- Enterprise Mode available (extra authentication required)

#### WPA2
- CCMP (802.11i, integrity check) and AES (i/o RC4)
- Personal Mode with PSK
- Enterprise Mode with centralized authentication

#### WPA3
- Introduced in 2018
- Personal Mode: CCMP128 as minimum
- Enterprise Mode: AES256 and SHA384
- Biggest Change: PSK removal
- Replacement: SAE (Simultaneous Authen of Equals) provides Forward Secrecy

#### NAC (Network Access Control)
- Permits/Denies NW access based on device characteristic
- Exp: OS, AV etc.
- Based on IEEE 802.1X standard
- As HW and SW solution available

#### Captive Portals (Hotel, Airport, Starbucks etc.)
- Appears before the user is able to access the NW
- Usually rely on 802.1x, which uses RADIUS for Authen

#### Geofencing
- Using GPS/RFID to define real-world boundaries
- Device can send alerts if it leaves the area

#### Disable SSID Broadcast (Server Set ID)
- Configures an AP to not broadcast SSID


## Others

#### WIFI Methods 
- Ad hoc: Peer to peer / directly (Exp: Bluetooth, Printer)
- Infrastructure: Not directly, but through WAP
- Channel Bonding: 
   - Used to reduce redundancy or increase throughput
   - Directly affecting the connection speed positively
