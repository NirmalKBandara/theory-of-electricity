---
# Laplace Transform - Transient Analysis
---
> *"What we know is not much, what we do not know is immense."*  
> — Pierre-Simon Laplace

## Introduction

The Laplace transformation is a mathematical tool that converts functions from the time domain to the complex frequency domain. This method can convert differential equations into simpler algebraic equations, making circuit analysis more manageable.

### Definition

The Laplace transform is defined as:

```
ℒ{f(t)} = F(s) = ∫₀^∞ f(t)·e^(-st) dt
```

Where:
- `f(t)` is the original time domain function
- `F(s)` is the transformed function in the s-domain
- `s = σ + jω` (complex frequency variable)

This method works because `e^(-st)` acts as a "weighting function" that extracts frequency information from `f(t)`. The weighting function multiplies different parts of our original function by different amounts, emphasizing some parts less and some parts more.

**Important Note:** This transformation is only defined for causal functions, where:
- `f(t) = 0` for all `t < 0`
- `f(t)` can be anything for `t ≥ 0`

## Laplace Inverse Transformation

The Laplace inverse transform is defined as:

```
f(t) = (1/2πj) ∫_{σ-j∞}^{σ+j∞} F(s)·e^(st) ds
```

However, we don't need to calculate in this manner. Instead, we generally obtain the inverse transform from tables that provide 's' to 't' conversions.

## System Analysis

In system analysis, the output in the s-domain is obtained by multiplying the transfer function and input function:

```
Y(s) = F(s) · U(s)
```

Where:
- `Y(s)` = Output (response) function
- `F(s)` = Transfer function
- `U(s)` = Input (excitation) function

## Properties of Laplace Transform

### 1. Linearity
**Forward Transform:**
```
ℒ{af₁(t) + bf₂(t)} = aF₁(s) + bF₂(s)
```

**Inverse Transform:**
```
ℒ⁻¹{aF₁(s) + bF₂(s)} = af₁(t) + bf₂(t)
```

### 2. Differentiation Property
**First derivative:**
```
ℒ{df(t)/dt} = s·F(s) - f(0⁺)
```

**Second derivative:**
```
ℒ{d²f(t)/dt²} = s²·F(s) - s·f(0⁺) - f'(0⁺)
```

**General nth derivative:**
```
ℒ{dⁿf(t)/dtⁿ} = sⁿF(s) - sⁿ⁻¹f(0⁺) - sⁿ⁻²f'(0⁺) - ... - f^(n-1)(0⁺)
```

### 3. Integration Property
```
ℒ{∫₀ᵗ f(t)dt} = F(s)/s
```

### 4. Value Theorems
**Initial Value Theorem:**
```
f(0⁺) = lim[t→0⁺] f(t) = lim[s→∞] s·F(s)
```

**Final Value Theorem:**
```
f(∞) = lim[t→∞] f(t) = lim[s→0] s·F(s)
```

### 5. Scaling Properties
**Time Scaling:**
```
ℒ{f(t/a)} = a·F(as)
```

**Frequency Scaling:**
```
ℒ⁻¹{F(s/a)} = a·f(at)
```

### 6. Multiplication by tⁿ
```
ℒ{tⁿ·f(t)} = (-1)ⁿ · dⁿF(s)/dsⁿ
```

### 7. Time Delay
```
ℒ{f(t-T)} = e^(-sT)·F(s)
```

### 8. Translation in s
```
ℒ⁻¹{F(s+a)} = e^(-at)·f(t)
```

## Common Excitation Functions

### Unit Impulse Function δ(t)
- **Definition:** Zero everywhere except at origin where it's infinite
- **Property:** ∫₋∞^∞ δ(t)dt = 1
- **Laplace Transform:** `ℒ{δ(t)} = 1`

### Unit Step Function u(t)
- **Definition:** 
  ```
  u(t) = {0, t < 0
          {1, t ≥ 0
  ```
- **Laplace Transform:** `ℒ{u(t)} = 1/s`

### Unit Ramp Function r(t)
- **Definition:**
  ```
  r(t) = {0, t < 0
          {t, t ≥ 0
  ```
- **Laplace Transform:** `ℒ{r(t)} = 1/s²`

### Polynomial Function y(t) = tⁿ
- **Laplace Transform:** `ℒ{tⁿ} = n!/s^(n+1)`

### Exponential Function y(t) = e^(-at)
- **Laplace Transform:** `ℒ{e^(-at)} = 1/(s+a)`

## Laplace Transform Tables

### Basic Functions
| Time Domain Function | Laplace Transform |
|----------------------|-------------------|
| Unit Impulse δ(t) | 1 |
| Unit Step u(t) | 1/s |
| Unit Ramp t | 1/s² |
| Polynomial tⁿ | n!/s^(n+1) |
| Exponential e^(-at) | 1/(s+a) |
| Sine Wave sin(ωt) | ω/(s²+ω²) |
| Cosine Wave cos(ωt) | s/(s²+ω²) |
| Damped Sine e^(-at)sin(ωt) | ω/[(s+a)²+ω²] |
| Damped Cosine e^(-at)cos(ωt) | (s+a)/[(s+a)²+ω²] |

### Advanced Functions
| Time Domain Function | Laplace Transform |
|----------------------|-------------------|
| Sinh Wave sinh(at) | a/(s²-a²) |
| Cosh Wave cosh(at) | s/(s²-a²) |
| Damped Sinh e^(-bt)sinh(at) | a/[(s+b)²-a²] |
| Damped Cosh e^(-bt)cosh(at) | (s+b)/[(s+b)²-a²] |
| (e^(-at) - e^(-bt))/(b-a) | 1/[(s+a)(s+b)] |
| (ae^(-at) - be^(-bt))/(a-b) | s/[(s+a)(s+b)] |

## The Laplace Inverse Transformation

The inverse transformation is generally obtained using tables of Laplace transform pairs. Before using the tables, we often need to rearrange the original transfer function in the s-domain using partial fraction expansion.

**F(s) is a rational function in s:**
```
F(s) = (Σᵢ₌₀ᵐ bᵢsᵢ)/(Σᵢ₌₀ⁿ aᵢsᵢ) = Numerator polynomial/Denominator polynomial
```

If the roots of the denominator polynomial are pᵢ, then:
```
F(s) = (Σᵢ₌₀ᵐ bᵢsᵢ)/(Πᵢ₌₁ʳ (s+pᵢ)^nᵢ)
```

### Example: Partial Fraction Expansion

Find the inverse Laplace transform of:
```
Y(s) = (s² + 2s + 2)/(s² + 3s + 2)
```

**Step 1:** Factor the denominator
```
Y(s) = (s² + 2s + 2)/[(s + 1)(s + 2)]
```

**Step 2:** Partial fraction expansion
```
Y(s) = k₀ + k₁/(s + 1) + k₂/(s + 2)
```

**Step 3:** Solve for coefficients
After algebraic manipulation:
```
Y(s) = 1 + 1/(s + 1) - 2/(s + 2)
```

**Step 4:** Inverse transform using tables
```
y(t) = δ(t) + e^(-t) - 2e^(-2t) for t > 0
```

## Transient Analysis using Laplace Transform

Instead of transforming time-domain differential equations to the s-domain, we can use the s-domain version of Ohm's law directly to write algebraic equations for circuits.

### Circuit Elements in s-Domain

| Element | Time Domain | s-Domain |
|---------|-------------|----------|
| Resistor | V = R·i | V(s) = R·I(s) |
| Inductor | V = L(di/dt) | V(s) = sL·I(s) - L·i(0⁺) |
| Capacitor | V = (1/C)∫i dt + V(0⁺) | V(s) = I(s)/(sC) + V(0⁺)/s |

### Circuit Analysis Example

**Problem:** RL Circuit with sinusoidal excitation
- Excitation voltage: Vs = 20sin(100t)
- R = 10Ω, L = 25mH
- Switch closed at t = 0

**Solution:**

**Step 1:** Transform to s-domain
```
Vs(s) = 2000/(s² + 10⁴)
```

**Step 2:** Write circuit equation
```
VL(s) = Ls·I(s) = Ls · Vs(s)/(R + Ls)
```

**Step 3:** Substitute values
```
VL(s) = 0.025s · 2000/(s² + 10⁴) · 1/(10 + 0.025s)
VL(s) = 2000s/[(s² + 100²)(s + 400)]
```

**Step 4:** Partial fraction and inverse transform
```
vL(t) = 4.706cos(100t) + 0.25sin(100t) - e^(-400t)
```

## The Problem-Solving Process

### Step 1: Take the Laplace Transform
Convert your differential equation to the s-domain using transform properties and tables.

### Step 2: Algebraic Manipulation
Use initial conditions and algebraic manipulation to solve for F(s). This often involves:
- Partial fraction expansion
- Completing the square
- Factoring polynomials

### Step 3: Inverse Transform
Use inverse Laplace transform tables to get f(t) from F(s).

## Historical Note

**Pierre-Simon Laplace (March 1749 – March 1827)** was a French scholar and polymath whose work was important to the development of engineering, mathematics, statistics, physics, and astronomy. Laplace formulated Laplace's equation and pioneered the Laplace transform, which appears in many branches of mathematical physics. The Laplacian differential operator is also named after him.

## Key Advantages

1. **Simplification:** Converts differential equations to algebraic equations
2. **Complete Solution:** Provides both transient and steady-state responses in a single formula
3. **Initial Conditions:** Automatically incorporates initial conditions into the solution
4. **System Analysis:** Enables easy analysis of complex systems using transfer functions
