## Premise System

- Used for building automation (BAS) 
- Exp: Door lock, CCTV, Elevator, HVAC
   - Consider process/memory vulns in PLC (!)
   - Plaintext credentials/Keys in application code (!)
   - Code injection via web user interface (!)
   - Denial of Service condition could be caused (!)

## PACS (Physical Access Control Security)
- Often installed/maintained by 3rd party supplier
- Thus often omitted during risk/vulnerability assessment by analysts!

## Surveillance
- CCTV (Closed Circuit TV)
- PTZ (Pan Tilt Zoom): Adjustable Camera
- Ultrasonic
- Infrared

## Door Locks
- Keys (Padlock)
- Pins (Cipher lock)
- Wireless signals
- Biometrics:
   - FAR (False Acceptance Rate):
       - False positive should be as low as possible
   - FRR (False Rejection Rate):
       - False negative
   - CER (Crossover Error Rate):
       - Equal error rate (EER) where FAR and FRR are equal

## Mantrap

- Area between two doorways that holds people until they are identified/authenticated

## Electrical Disturbance Prevention

1. Surge: unexpected increase of voltage provided
2. Spike: short transient in voltage due to short circuit/power outage
3. Sag: opposite of Surge
4. Brownout: opposite of Spike (causes lights to dim )
5. Blackout: total loss of power

**BackUp Power Supply**
1. UPS (Uninterruptible Power Supply): Surge protecter & battery backup
2. Backup Generator: In case of power outage
