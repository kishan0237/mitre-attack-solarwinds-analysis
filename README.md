# MITRE ATT&CK Analysis: SolarWinds SUNBURST

A small case study of the 2020 SolarWinds Orion supply-chain compromise, using the MITRE ATT&CK Enterprise framework to organize the attacker behavior described in public reports.

## Why I made this

I wanted to practice reading an incident report and turning the technical details into ATT&CK mappings. The goal is not to reproduce the whole incident, but to understand how a SOC analyst can move from an observed behavior to a tactic and technique.

## Incident

- **Incident:** SolarWinds Orion supply-chain compromise
- **Malware:** SUNBURST
- **MITRE campaign:** C0024
- **MITRE software:** S0559
- **Time period:** 2020
- **Type:** Supply-chain compromise

## Short incident summary

Attackers compromised part of the SolarWinds software build process and inserted malicious code into Orion software. Affected Orion updates were then distributed to customers through the normal software update mechanism.

After an affected update was installed, the SUNBURST backdoor could execute on the victim system and communicate with attacker-controlled infrastructure. The malware performed system checks and collected information that could help determine whether the host was worth further activity.

This makes the incident useful for learning both supply-chain compromise and post-compromise discovery/C2 behavior.

## ATT&CK mapping

| Tactic | Technique | ID | What happened |
|---|---|---|---|
| Initial Access | Compromise Software Supply Chain | T1195.002 | Malicious code was inserted into the Orion software build and distributed through trusted updates. |
| Defense Evasion | Obfuscated Files or Information | T1027 | SUNBURST contained obfuscated functionality used to make analysis and detection harder. |
| Discovery | Process Discovery | T1057 | SUNBURST gathered information about running processes. |
| Discovery | Query Registry | T1012 | SUNBURST queried the Windows Registry for information about the host. |
| Discovery | Security Software Discovery | T1518.001 | SUNBURST checked for security software on the system. |
| Command and Control | Application Layer Protocol: Web Protocols | T1071.001 | SUNBURST used web protocols for C2 communication. |
| Command and Control | Application Layer Protocol: DNS | T1071.004 | DNS was used as part of the malware's C2 mechanism. |
| Collection | Data from Local System | T1005 | The malware could collect information from the local system. |

## Attack flow

```text
SolarWinds build environment compromised
                |
                v
       Malicious code inserted
                |
                v
        Orion update released
                |
                v
       Customer installs update
                |
                v
          SUNBURST runs
                |
        +-------+-------+
        |               |
        v               v
 System discovery     C2 communication
        |               |
        +-------+-------+
                |
                v
       Further attacker activity
```

## One mapping explained

### T1195.002 — Compromise Software Supply Chain

The important point here is that the attacker did not need to compromise every victim separately. The trusted software distribution mechanism became the path to the victim.

**Tactic:** Initial Access  
**Technique:** T1195.002  
**Technique name:** Compromise Software Supply Chain

This is a good example of why software build systems, update mechanisms and code-signing processes are important security boundaries.

## What I would look for as a defender

For a similar environment, useful investigation points would include:

- Unexpected changes in software build pipelines
- Integrity checks for build artifacts
- Unusual outbound connections from management servers
- Unexpected DNS activity
- Suspicious use of trusted software processes
- Endpoint telemetry showing unusual discovery behavior
- Changes to signing or release processes
- Whether the installed software version matches the approved release

## Sources

1. MITRE ATT&CK — SolarWinds Compromise (C0024)  
   https://attack.mitre.org/campaigns/C0024/

2. MITRE ATT&CK — SUNBURST (S0559)  
   https://attack.mitre.org/software/S0559/

3. CISA — Advanced Persistent Threat Compromise of Government Agencies, Critical Infrastructure, and Private Sector Organizations  
   https://www.cisa.gov/news-events/cybersecurity-advisories/aa20-352a

## Disclaimer

This is an educational analysis based on publicly available incident information. I did not access SolarWinds systems or perform testing against the affected infrastructure.

## Skills practiced

- MITRE ATT&CK
- Incident analysis
- Threat intelligence basics
- Tactic and technique mapping
- Security event interpretation
- Basic SOC detection thinking
