# Blue Team

<br />

## Threat Analysis
1. Threat Modeling: Understand every component, interconnection, use case
   1. Description of the system (NW, Website, Cloud, App)
   2. Analyze the technical background (UML sequence diagrams)
   3. Determine Threats 
      - Consider inside/outside threats
      - Consider Adversary Capability: Developed, Advanced, Integrated
      - Consider Attack Vector: Cyber, Human, Physical
      - Who uses the system?
      - How do they get access?
      - What are the privilege levels?
      - How does information flow and what is the value of it?
   4. Determine Vulnerabilities
   5. Prioritize threats (Risk Management)
2. Asset Mapping: Prioritize the identified assets by assigning value to assets
3. Risk Management: Calculate risk scores, prioritize risks
4. Mitigation Plan: Propose set of most cost-effective countermeasures

![grafik](https://user-images.githubusercontent.com/84674087/132233377-3f395401-7edd-44f3-ba7a-ab9744706ccc.png)

## What is a suspicious process? (Threat Modeling)
- Any process you don't recognize
- Any process similar to legitimate process, e.g. scvhost.exe
- Any process w/o icon, version info, description etc
- Any process that are unsigned
- Any process whose digital signature doesn't match
- Any process w/o parent/child but with principle Windows process
- Any process that is packed, highlighted in purple in explorer window

## What to do after detection of suspicious process?
- Identify how it interacts with Registry and file system?
- How did it launch?
- Image file located in system folder (trustworthy) or temp folder?
- What files are being manipulated?
- Does it restore itself upon reboot after deletion?
- Does system privilege/service get blocked if you delete process?
- Is it interacting with the network?

**> Many UEBA products can automate this processes**
