The concept of catchment response time does not have a unique definition and cannot be directly measured as a single physical quantity. Instead, it represents an emergent property of the rainfall–runoff relationship, reflecting how a catchment transforms input signals into output responses over time.

Different methodological approaches can be used to estimate this characteristic timescale, each relying on specific assumptions about system behavior, such as linearity, stationarity, and the relative importance of storage and flow pathways. As a result, the estimated response time may vary depending on the method adopted and should be interpreted accordingly.

In complex systems, particularly those characterized by strong storage effects or multiple flow components (e.g., karst environments), the response time should not be understood as a single travel time, but rather as an effective timescale integrating multiple processes.


# DMCA and Catchment Response Time — Structured Explanation

## The problem

Giani et al. address a key limitation of classical hydrology: the definition of a representative response time of a catchment. The traditional time of concentration (Tc) is based on geometry and idealized assumptions, and it becomes unreliable in real, complex systems. See Beven (2020) => insted of the particle velocity we should use the wave propagation celerity.

The shift proposed is conceptual: instead of asking how long water takes to travel, the question becomes:

> At what temporal scale are rainfall and streamflow linked?

This leads to the idea of a **catchment response time (Tr)** as a system property.


N.B. Tr based on hourly time series with any assumptions.

---

## Why classical methods are not sufficient

Rainfall and streamflow behave very differently:

- Rainfall → high-frequency, impulsive
    
- Streamflow → smoother, delayed
    

Using cross-correlation requires smoothing rainfall, which alters:

- timing
    
- peaks
    
- signal structure
    

DMCA  (Kristoufek, 2015) avoids this by working directly on the original data.

---

## How the DMCA method works (conceptually)

The method can be understood in three main steps.

### 1. Integration

Rainfall and streamflow are transformed into cumulative series. This highlights large-scale behavior and reduces noise.

### 2. Detrending

A centered moving average of length L is applied and subtracted:

fluctuation = cumulative − moving average

These fluctuations:

- can be positive or negative
    
- represent deviations from the local trend
    

### 3. Correlation across scales

The correlation between rainfall and streamflow fluctuations is computed for different values of L.



[github code](https://github.com/giuliagiani/Tr_DMCA)
---

## What “fluctuations” really represent

A key clarification:

Fluctuations are not the original signal.

They represent:

> how the signal deviates from its local behavior

Interpretation:

- negative → before the main contribution
    
- positive → after the main contribution
    
In the DMCA approach, the minimum of the correlation function does not indicate a weaker relationship between precipitation and discharge, but rather identifies the temporal scale at which their common dynamics is best captured, after removing the dominant trend, and the residual fluctuations are least correlated.



---

## The “center of mass” concept

The method refers to a center of mass, but this should not be interpreted physically.

It is more accurate to say:

> it is the temporal center of the fluctuations

This corresponds to the point where fluctuations change sign.

For each event:

- rainfall has a center (t_R)
    
- streamflow has a center (t_Q)
    

Their difference defines an event-based response time.

---

## Why this is not enough

If we stop here, each event gives a different value of Tr.

The goal is instead:

> to obtain a single characteristic timescale of the basin

---

## The key mechanism of DMCA

Between the two centers (t_R → t_Q):

- rainfall fluctuations are positive
    
- streamflow fluctuations are negative
    

Their product is negative.

If a moving window fully covers this interval:

→ the correlation becomes strongly negative

---

## The critical result

The strongest negative correlation occurs when:

L ≈ 2 Tr

This leads to:

Tr = (L_min − 1) / 2

Explanation:

- the window is centered
    
- it must span the full delay between rainfall and response
    

The term (L − 1)/2 comes from the discrete structure of the window.

---

## Important conceptual distinctions

- Lag → time shift between signals
    
- Timescale → scale at which signals become related
    

DMCA identifies a **timescale**, not a single lag.

---

## Critical observation: karst systems

In karst basins:

- strong storage
    
- multiple flow paths
    
- nonlinear processes

In particular, if water is temporarily stored, redistributed, or released through different pathways and timescales, to what extent can the assumption of a coherent and conserved contribution—implicit in the notion of a center of mass—still be considered valid?


---

## Technical clarifications

- Number of windows = T − L + 1
    
- Window is centered → leads to (L − 1)/2
    
- Intersection between moving average and cumulative series:
    
    - not invariant with L
        
    - only stable in ideal symmetric cases
        
- **Rising limb**  
    Increasing part of the hydrograph after rainfall.
- **Recession limb**  
    Decreasing part of the hydrograph.


---

## Final interpretation

The DMCA method does not estimate a physical travel time.

It provides:

> the dominant temporal scale at which rainfall and runoff are coupled


---

## References

Beven, K. (2020). _Rainfall-Runoff Modelling: The Primer_ (2nd ed.). Wiley.

Giani, A., et al. (2020). A Practical, Objective, and Robust Technique to Directly Estimate Catchment Response Time. _Water Resources Research_, 56, e2020WR028201.

Kristoufek, L. (2015). Power-law cross-correlations estimation under heavy tails. _Communications in Nonlinear Science and Numerical Simulation_, 20(2), 342–351.

McCuen, R. H. (2009). _Hydrologic Analysis and Design_ (3rd ed.). Pearson.

---

End.
