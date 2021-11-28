# Blue Team

*STIX (Structured Threat Information eXpression): Standard terminology for IOCs (in JSON)*

<br />

## SDOs (STIX Domain Objects)
- Content:
   - Observed Data
   - Indicator
   - Attack Pattern
   - Campaign and Threat Actors
   - Course of Action (COA)

## TAXII (Trusted Automated eXchange of Indicator Information):
- Protocol for supplying codified information to automate analysis
- Between server and clients over secure connection (like REST API)
- STIX could be sent via TAXII

## OpenIOC
- Framework that uses XML-formatted files
- For supplying codified information

## MISP (Malware Information Sharing Project)
- Platform for Cyber Threat Intelligence Sharing
- Proprietary format, but open source project
- Supports OpenIOC
- Can import/export STIX over TAXII
