# ATT&CK Mapping Notes

## T1195.002 - Compromise Software Supply Chain
**Tactic:** Initial Access

The SolarWinds case is a useful example of a trusted software update being used as the delivery path for malicious code.

## T1027 - Obfuscated Files or Information
**Tactic:** Defense Evasion

SUNBURST used obfuscation in parts of its implementation. In an investigation, this is relevant because static analysis of the malicious component can be made more difficult.

## T1057 - Process Discovery
**Tactic:** Discovery

SUNBURST gathered information about processes on the infected host.

## T1012 - Query Registry
**Tactic:** Discovery

The malware queried the Windows Registry to collect information from the host.

## T1518.001 - Security Software Discovery
**Tactic:** Discovery

SUNBURST checked for security products. This type of behavior can help an attacker understand the defensive environment.

## T1071.001 - Application Layer Protocol: Web Protocols
**Tactic:** Command and Control

The malware used web protocols for communication with its C2 infrastructure.

## T1071.004 - Application Layer Protocol: DNS
**Tactic:** Command and Control

DNS was incorporated into the SUNBURST communication mechanism.

## T1005 - Data from Local System
**Tactic:** Collection

The malware could collect information from the local host.

## Analyst takeaway

The useful part of ATT&CK mapping is not memorizing IDs. The process is:

**incident evidence -> attacker behavior -> ATT&CK technique -> tactic -> possible detection**

For example:

**"malware checks running processes" -> Process Discovery -> T1057 -> Discovery**

That is the workflow practiced in this case study.
