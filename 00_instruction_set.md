
# 00 — Instruction Set

Home Assembly (HA) is a low-level, mode-sensitive, state-resolved execution system.

An instruction is not a command word. It is a resolved event.

```
I = f(x, y, M, k, s, w, b)
```

where:

- `(x, y)` = raw event pair
- `M` = current interpretation mode
- `k` = cartridge state
- `s` = slot position
- `w` = switch state
- `b` = button/interface state


---

## 1. Machine state vector

```
σ = ⟨X, Y, C, K, S, W, B, M, P, E⟩
```

| Symbol | Meaning |
|--------|---------|
| `X` | X-plane state |
| `Y` | Y-plane state |
| `C` | synthesis controller |
| `K` | cartridge state space |
| `S` | slot topology |
| `W` | switch state |
| `B` | button/input state |
| `M` | interpretation mode |
| `P` | operand precedence |
| `E` | executable world state |


---

## 2. Primitive event form

The primitive input is an ordered pair:

```
e = (x, y)     where x, y ∈ {0 .. 18}
```

The same pair does not denote one fixed thing. It denotes a family of possible instructions whose resolution depends on machine mode.

The decode function is:

```
δ(σ, e) = ι
```

where `ι` is the resolved instruction object.


---

## 3. Decode table

| Mode `M` | Event `e = (x, y)` | Condition | Decoded instruction `ι` |
|----------|-------------------|-----------|------------------------|
| `M_pair` | `(x, y)` | x ≠ 0, y ≠ 0 | `Coord(x, y)` |
| `M_x` | `(x, 0)` | x ≠ 0 | `SelectEntity(x)` |
| `M_y` | `(0, y)` | y ≠ 0 | `ModifyState(y \| x)` |
| `M_sync` | `(x, y)` | any | `SynthesizeOp(C(x, y, σ))` |
| `M_pass` | `P` | — | `ControlEvent(pass)` |
| `M_slot` | `(x, y)` | slot-bound `k` present | `SlotBound(S_n(k), x, y)` |

Precedence-sensitive variants:

| Precedence `P` | Effect on decode |
|---------------|-----------------|
| `X ≺ Y` | X operand is primary; Y modifies |
| `Y ≺ X` | Y operand is primary; X modifies |

Precedence is mutable. It flips at awakening threshold `t_awakening`.

```
t_awakening  →  P := Y ≺ X
```

Therefore:

```
δ(σ, (x, y), P = X≺Y)  ≠  δ(σ, (x, y), P = Y≺X)
```

The same pair resolves differently across machine phases.


---

## 4. Mode register

```
M ∈ { M_pair, M_x, M_y, M_sync, M_pass, M_slot, M_switch }
```

Mode is not secondary. Mode is part of the ontology of the instruction.

```
(x, y)         ≠  instruction by itself
(x, y, M)      =  instruction
```


---

## 5. Zero as axis-suppression operator

Zero is not a value. Zero is a read discipline.

```
(x, 0)   →  read X in isolated mode   →  SelectEntity(x)
(0, y)   →  read Y in isolated mode   →  ModifyState(y)
```

Therefore:

```
0  =  axis-suspension operator
```

Zero selects interpretive depth, not absence.


---

## 6. Pass as control event

Pass is not null. Pass is not silence.

```
P  →  ControlEvent
```

Pass may produce any of:

- mode retention
- priority shift
- execution delay
- safety preservation
- suspension of issue


```
P  ≠  ∅
P  =  meaningful non-placement event
```


---

## 7. Reserved coordinates (opcode-coordinate overlap)

Certain coordinates carry executive force regardless of mode.

```
(7, 7)    →  Wake(p)          — awakens current target cartridge
(10, 10)  →  Shutdown(Home)   — absorbing safety state; hard collapse
(11, 11)  →  Ignition         — boot origin; black opening command
```

These coordinates are members of both coordinate-space and instruction-space:

```
Coordinate ∩ Opcode ≠ ∅
```

`(10, 10)` is an absorbing state:

```
∀s,  Reach(s, 10, 10)  →  terminate
NextState = Off
```


---

## 8. Boot sequence as first sentence

Boot is not pre-linguistic. Boot is grammar.

```
(11, 11)  →  Ignition
(7, 7)    →  Wake
Ack       →  "system coherent; proceed"
P         →  PriorityShift   (X≺Y → Y≺X)
```

This is the machine's first sentence.


---

## 9. Transition system (partial)

Let `→` denote state transition under event `e` given `σ`.

```
σ  —e→  σ'
```

Selected transitions:

```
σ_off    —(11,11)→   σ_ignition
σ_ign    —(7,7)→     σ_awake
σ_awake  —Ack→       σ_ready
σ_ready  —P→         σ_shifted        (precedence flips)
σ_any    —(10,10)→   σ_off            (absorbing)
```

Illegal state handling:

- cartridge absent from expected slot: `→ σ_fault`
- slot conflict: `→ σ_fault`
- missing synthesis conditions: `→ σ_stall`

Fault states must be explicit and recoverable unless `(10, 10)` is reached.


---

## 10. Instruction in one sentence

```
HA  =
a low-level, mode-sensitive, state-resolved assembly in which instructions emerge
from paired and isolated reads across dual domains, are synthesized by a temporary
execution controller, and are modified by cartridge state, slot topology, switch
conditions, and live human interaction.
```

Compressed:

```
instruction  =  resolved relation
zero         =  axis isolation
controller   =  execution join
pass         =  control event
slot         =  operator
cartridge    =  stateful participant
coordinate   =  possible opcode
play         =  runtime scripting
```
