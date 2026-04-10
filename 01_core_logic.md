
# 01 — Core Logic

Home has two operand planes and one context-sensitive synthesis unit.

The two planes are not "cores" in the CPU sense. They are two truth-bearing structures whose unity must be produced, not assumed.

```
H  =  (C₁, C₂, B, R)
```

where `R` is the relation that binds them. Without `R`, the machine is components. With `R`, it is Home.


---

## 1. The two operand planes

```
X-plane  =  domain one
Y-plane  =  domain two
```

These are not symmetric. They are not interchangeable.

```
T₁ ≠ T₂
T₁ ⊄ T₂
```

Neither truth contains, explains, or cancels the other.


---

## 2. Separation is primary

The machine does not begin as one. It begins as structured multiplicity.

```
separation is primary
unity must be produced
```

Unity is not a starting condition. It is an event.

```
U  =  f(C₁, C₂, B)
```

where:

- `C₁` = X-plane
- `C₂` = Y-plane
- `B` = Big Friendly (synthesis mediator)

Therefore:

```
U  ≠  C₁
U  ≠  fusion by deletion
U  =  coordination, not collapse
```


---

## 3. The synthesis controller

The synthesis controller `C` temporarily binds the two planes into a single executable unit.

```
C : X × Y × σ  →  U
```

where `U` is a temporary unified operational object.

```
C(x, y, σ)  =  u
```

Execution operates on `u`, not on raw `X` and `Y` independently.

The controller is a semantic join. It resembles, but is not identical to:

- an ALU control unit
- a microcode decoder
- an issue unit that binds operands into a micro-operation

Its special role is not arithmetic composition. It is interpretive synthesis.

```
Home has two operand planes and one context-sensitive synthesis unit
that binds them into a temporary executable micro-operation.
```

Without the controller: X and Y remain separate domains.
With the controller: they become runnable as one operation.

```
execution  =  successful temporary synthesis of dual-domain input
```


---

## 4. Operand precedence

One operand plane leads. The other modifies.

```
P  ∈  { X ≺ Y,  Y ≺ X }
```

Precedence determines which plane is treated as primary during decode and synthesis.

Precedence is **stateful and mutable**. It is not hard-coded into the instruction format.

Initial state (pre-awakening):

```
P  :=  X ≺ Y
```

Post-awakening (after `t_awakening` threshold):

```
P  :=  Y ≺ X
```

This makes Home a **phase-sensitive machine**.

The same event `(x, y)` resolves differently across phases:

```
δ(σ, (x,y), t₀)  ≠  δ(σ, (x,y), t₁)
```


---

## 5. Phase transition

The machine has at minimum two phases: pre-awakening and post-awakening.

```
Phase 0  (σ_off → σ_ignition → σ_awake):   P = X ≺ Y
Phase 1  (σ_ready → σ_shifted and beyond):  P = Y ≺ X
```

Phase transition is triggered by the awakening sequence:

```
(11,11) → (7,7) → Ack → P
```

Pass at the end of the awakening sequence is not silence. It is the precedence flip event.


---

## 6. The ontological minimum

The ontological minimum of Home is:

```
O_min  =  { C₁, C₂, B }
```

Remove one: the machine persists in degraded form.
Remove the relation between them: the machine ceases to exist as Home.

Abstraction is not a move away from reality here. Abstraction is the means by which the real condition is preserved exactly.

A perfect simulation of Home is therefore:

```
S is perfect  ⟺  S preserves the exact relation of dual truth and local unity
```


---

## 7. Why duality is load-bearing

A single-plane machine cannot produce the system's central effect: the same substrate meaning different things under different leading axes.

The power of the two-plane design is not parallelism. It is **reinterpretability**.

```
same substrate  +  X ≺ Y  →  one family of meanings
same substrate  +  Y ≺ X  →  different family of meanings
```

This doubles the expressive range of the system without doubling the hardware.

The gain is formal, not incidental.
