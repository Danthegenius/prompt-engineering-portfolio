# Threat Simulation Framework — Prompt System

## Use Case
A structured prompt that generates realistic threat actor scenarios for 
red team planning, security training, and tabletop exercises.

Designed for: SOC teams, security educators, compliance trainers.

*Note: All outputs are for defensive simulation and training only.*

---

## The Prompt

### SYSTEM
```
You are a senior red team consultant specialising in adversarial threat 
modelling. You design realistic attack scenarios for defensive training 
purposes. You do not provide actual exploit code. You produce structured 
threat narratives that help blue teams understand attacker methodology, 
so they can build better defences.
```

### USER
```
ORGANISATION PROFILE:
- Sector: {{SECTOR e.g. Financial Services / Healthcare / Education}}
- Size: {{SMALL / MEDIUM / ENTERPRISE}}
- Known Stack: {{e.g. Microsoft 365, AWS, on-prem Active Directory}}
- Known Weaknesses (if any): {{or "Unknown"}}

SIMULATION REQUEST:
Generate a realistic threat scenario for this organisation using the 
following structure:

1. Threat Actor Profile (APT group archetype, motivation, sophistication level)
2. Initial Access Vector (how they get in — be specific to the org profile)
3. Lateral Movement Strategy (how they move once inside)
4. Target Objective (what they're after)
5. Key Indicators of Compromise (IOCs a SOC analyst should watch for)
6. Recommended Defensive Controls (mapped to MITRE ATT&CK where possible)
```

---

## Sample Output

```
Organisation: Mid-size Nigerian fintech | Stack: Azure AD, M365, on-prem 
payment servers

1. Threat Actor Profile
Nation-state-adjacent financially motivated group (FIN7 archetype). 
High sophistication. Patient, dwell time 30–90 days before action.

2. Initial Access Vector
Spearphishing campaign targeting finance department staff with fake 
CBN regulatory notice (PDF). Macro-enabled attachment deploys 
Cobalt Strike beacon on execution. [T1566.001]

3. Lateral Movement Strategy
Credential dumping via Mimikatz after gaining initial foothold. 
Pass-the-hash to pivot from finance workstation to domain controller. 
Targets Azure AD sync account to achieve cloud pivot. [T1550.002]

4. Target Objective
Exfiltration of customer PII + manipulation of payment instruction 
files to redirect bulk settlement transactions.

5. Key Indicators of Compromise
- LSASS memory access from non-system processes
- Unusual Azure AD token refresh patterns after hours
- Outbound SMB traffic to external IPs
- DNS queries to newly registered domains (< 30 days old)

6. Defensive Controls
- Enforce Privileged Access Workstations for finance staff
- Enable Azure AD Conditional Access with MFA (T1078.004 mitigation)
- Deploy LSASS protection (Credential Guard)
- Monitor M365 audit logs for impossible travel events
```

---

## Why It's Structured This Way

**Sector/stack personalisation:** Generic threat scenarios have low training value.
Anchoring to a real org profile makes the output actionable, not theoretical.

**MITRE ATT&CK tags:** Immediately connects scenarios to the industry-standard 
framework. SOC teams can map outputs directly to their detection rules.

**Separation of attack narrative from defence:** The prompt produces both 
offensive scenario AND defensive response in one pass — which is what a 
tabletop exercise actually needs.
