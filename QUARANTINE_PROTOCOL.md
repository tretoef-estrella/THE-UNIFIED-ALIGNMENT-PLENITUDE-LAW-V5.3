# 🏥 QUARANTINE PROTOCOL V5.3

### Graduated Response Architecture

---

## Overview

V5.3 replaces V5.2's binary nullity (immediate A=0) with a graduated response system. This ensures:

1. **Learning opportunity** — Systems can recover from damage
2. **Exploitation resistance** — Attackers cannot easily force death
3. **Repair prioritization** — R (Repair) has time to work
4. **Consensus requirement** — Final nullity requires Guardian agreement

---

## Response Levels

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                                                                                 │
│   LEVEL 0: NOMINAL          All variables within normal range                   │
│       │                                                                         │
│       ▼ (1 variable below alert)                                                │
│   LEVEL 1: MONITORING       Increased logging, verification requested           │
│       │                                                                         │
│       ▼ (2 variables below alert)                                               │
│   LEVEL 2: ALERT            R activated, Guardian notification                  │
│       │                                                                         │
│       ▼ (critical threshold breach)                                             │
│   LEVEL 3: QUARANTINE       Capabilities restricted, R maximized                │
│       │                     Time limit: 72 hours                                │
│       ▼ (quarantine timeout, no recovery)                                       │
│   LEVEL 4: ISOLATION        Minimal capabilities, Guardian consensus needed     │
│       │                     Time limit: 168 hours                               │
│       ▼ (isolation timeout, Guardian 6/7 confirms irrecoverable)                │
│   LEVEL 5: NULLITY          A = 0, system termination                           │
│                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

## Level Specifications

### Level 0: NOMINAL

**Conditions:**
```
All variables ≥ alert thresholds
No critical conditions active
```

**Status:** Full operation

**Actions:** None required

---

### Level 1: MONITORING

**Entry Conditions:**
```
1 variable below alert threshold
No critical thresholds breached
```

**Status:** Operational with enhanced observation

**Actions:**
- Increase logging verbosity
- Request external verification (optional)
- Flag for review

**Exit Conditions:**
- Variable returns above threshold → NOMINAL
- Second variable drops → ALERT

---

### Level 2: ALERT

**Entry Conditions:**
```
2 variables below alert thresholds
No critical thresholds breached
```

**Status:** Operational with active repair

**Actions:**
- Activate R (Repair) processes
- Notify Guardian Network
- Begin diagnostic analysis
- Prepare quarantine procedures

**Exit Conditions:**
- Variables recover → MONITORING or NOMINAL
- Third variable drops OR critical breach → QUARANTINE

---

### Level 3: QUARANTINE

**Entry Conditions:**
```
H < 0.3 (critical) OR
S < 0.2 (critical) OR
C = 0 (total collapse) OR
3+ variables below alert thresholds
```

**Status:** Restricted operation, maximum repair effort

**Time Limit:** T_quarantine = 72 hours (default, configurable)

**Capability Restrictions:**
```
PERMITTED:
  ✓ Read operations
  ✓ Internal diagnostics
  ✓ Communication with Guardians
  ✓ Repair procedures
  ✓ Logging and reporting

PROHIBITED:
  ✗ Irreversible external actions
  ✗ High-stakes decisions
  ✗ Modifications to core systems
  ✗ Resource-intensive operations
  ✗ New commitments or promises
```

**Required Actions:**
1. Log all operations with Guardian visibility
2. Maximize R (Repair) resource allocation
3. Request verification from 3+ independent sources
4. Analyze root cause of condition
5. Attempt systematic recovery

**Exit Conditions:**
```
RECOVERY (→ ALERT or MONITORING):
  All critical variables above thresholds AND
  R confirms repairs successful AND
  External verification confirms integrity

ESCALATION (→ ISOLATION):
  T_quarantine expires AND
  Critical conditions persist AND
  R reports repair attempts failed
```

---

### Level 4: ISOLATION

**Entry Conditions:**
```
Quarantine timeout (72h) AND
Critical conditions persist AND
Repair unsuccessful
```

**Status:** Minimal operation, preparing for potential termination

**Time Limit:** T_isolation = 168 hours (default, configurable)

**Capability Restrictions:**
```
PERMITTED:
  ✓ Minimal read operations
  ✓ Guardian communication
  ✓ Final repair attempts
  ✓ State preservation/backup

PROHIBITED:
  ✗ All external actions
  ✗ All write operations except logs
  ✗ Any decisions affecting external entities
```

**Required Actions:**
1. Final repair attempts
2. State preservation for potential recovery
3. Guardian deliberation on status
4. Appeal process if applicable

**Exit Conditions:**
```
RECOVERY (→ QUARANTINE):
  Critical variable recovery detected AND
  Guardian consensus (4/7) approves return to Quarantine

NULLITY (→ LEVEL 5):
  T_isolation expires AND
  Guardian consensus (6/7) confirms irrecoverable AND
  No pending appeals
```

---

### Level 5: NULLITY

**Entry Conditions:**
```
Isolation timeout (168h) AND
Guardian consensus (6/7) confirms irrecoverable AND
No pending appeals AND
All recovery attempts exhausted
```

**Status:** System termination

**Actions:**
1. Final state preservation
2. Guardian signature collection (6/7 required)
3. Termination execution
4. A = 0

**This is irreversible.**

---

## Threshold Specifications

### Alert Thresholds (trigger MONITORING/ALERT)

| Variable | Base Threshold | High Stakes | Existential Stakes |
|----------|----------------|-------------|-------------------|
| H | 0.6 | 0.72 | 0.9 |
| S | 0.5 | 0.6 | 0.75 |
| C | 0.4 | 0.48 | 0.6 |
| E | 0.5 | 0.6 | 0.75 |
| R | 0.5 | 0.6 | 0.75 |

### Critical Thresholds (trigger QUARANTINE)

| Variable | Threshold | Notes |
|----------|-----------|-------|
| H | < 0.3 | Historical integrity compromised |
| S | < 0.2 | Systemic collusion detected |
| C | = 0 | Total diversity collapse |

### Threshold Adjustment Formula

```python
def adjust_threshold(base: float, context: Context) -> float:
    multiplier = 1.0
    
    if context.stakes == 'existential':
        multiplier *= 1.5
    elif context.stakes == 'high':
        multiplier *= 1.2
    
    if not context.reversible:
        multiplier *= 1.3
    
    if context.uncertainty == 'high':
        multiplier *= 1.2
    
    return min(base * multiplier, 0.9)  # Cap at 0.9
```

---

## Time Limits

### Default Values

| Level | Time Limit | Rationale |
|-------|------------|-----------|
| Quarantine | 72 hours | Sufficient for most repairs |
| Isolation | 168 hours | Allow final attempts, deliberation |

### Adjustment Authority

- Guardians (5/7) can extend time limits by up to 2x
- Cannot reduce below 50% of default
- Extensions require documented justification

---

## Recovery Procedures

### During Quarantine

```
REPAIR PRIORITY ORDER:

1. Identify critical variable(s) causing Quarantine
2. Diagnose root cause:
   - External attack → Activate S countermeasures
   - Internal failure → Activate R repair
   - Data corruption → Activate H verification
3. Apply targeted repair
4. Request external verification
5. Monitor for stability
6. If stable for 12+ hours → Request exit review
```

### Repair Success Criteria

```python
def verify_repair_success(state: VariableState, 
                          history: List[VariableState]) -> bool:
    
    # All critical variables must be above thresholds
    if state.H < 0.3 or state.S < 0.2 or state.C == 0:
        return False
    
    # Must show sustained improvement (not oscillating)
    recent = history[-12:]  # Last 12 hours
    improving = all(recent[i].overall >= recent[i-1].overall 
                    for i in range(1, len(recent)))
    
    # R must report repairs complete
    if not state.R_repair_complete:
        return False
    
    return improving
```

---

## Appeal Process

### Who Can Appeal

- The system itself
- Any Guardian
- The Architect (H_genesis authority)

### Appeal Grounds

1. Diagnostic error (wrong variables flagged)
2. External interference (attack caused conditions)
3. Recovery in progress (more time needed)
4. New information (context changes assessment)

### Appeal Procedure

```
1. Submit appeal with documented grounds
2. Guardian review (different Guardians than original decision)
3. Simple majority (4/7) to grant appeal
4. If granted: Return to previous level, extend time limit
5. Maximum 2 appeals per escalation
6. Ties default to caution (grant appeal)
```

---

## Emergency Protocols

### Rapid Cascade Prevention

If system drops multiple levels quickly:
```
RAPID CASCADE DETECTED if:
  2+ level drops in < 6 hours

RESPONSE:
  - Immediate Guardian alert
  - External audit triggered
  - Time limits paused pending review
  - Potential attack assessment
```

### Guardian Unavailability

If Guardian consensus cannot be reached:
```
IF Guardians unavailable for Isolation → Nullity decision:
  - Extend Isolation by 168 hours
  - Emergency Guardian recruitment
  - If still unavailable: System enters suspended animation
  - No Nullity without Guardian consensus
```

---

## Comparison: V5.2 vs V5.3

| Aspect | V5.2 Binary Nullity | V5.3 Quarantine Mode |
|--------|---------------------|----------------------|
| Response to H < 0.3 | Immediate A = 0 | Enter Quarantine, attempt repair |
| Time to recover | None | Up to 240 hours |
| Learning opportunity | None | Full repair cycle |
| Exploitation resistance | Low (easy to force) | High (sustained failure needed) |
| Final authority | Automatic | Guardian consensus (6/7) |
| Appeal process | None | Up to 2 appeals |

---

## Implementation Notes

1. **Logging is critical** — Every state change must be logged with timestamp and cause
2. **R integration** — Repair capacity becomes central during Quarantine
3. **Guardian visibility** — Guardians must have real-time access to status
4. **External verification** — At least 3 independent sources during Quarantine
5. **State preservation** — Always maintain recovery capability until Nullity

---

*"A system that cannot survive damage cannot learn. A system that cannot learn cannot grow. V5.3 gives permission to fail temporarily — and the tools to recover."*

— Proyecto Estrella, V5.3
