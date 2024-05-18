# geom_archetypal
## Geometrical Archetypal Analysis

Overview
--------

geom_archetypal is a Python Module for performing Grid Archetypal Analysis (GAA) by using
a properly modified version of the PCHA algorithm.

Basic functions are:

-   `fast_archetypal()` Archetypal Analysis (AA) with given data rows as archetypes
-   `grid_archetypal` For a data matrix n x d finds the Grid Archetypes and performs AA
-   `closer_grid_archetypal` For a data matrix n x d finds the Closer Grid Archetypes and performs AA
-   `archetypal_pcha()` Principal Convex Hull Analysis (PCHA)

Installation
------------
On the terminal of your operating system write and press enter:

```python
$ pip install geom_archetypal
```

Usage
-----
```python
# Load Module:
from geom_archetypal import *
# Set seed:
seed=20240518
np.random.seed(seed)
# Create random data
n=100
d=2
df = np.random.random((n, d))
# grid_atrchetypal()
BY, A, B, AM, AMDF, SSE, varexpl, fin_iters, time_elapsed, diagsum_final = (
    grid_archetypal(df,  diag_less = 1e-6, verbose = True))
pd.DataFrame(BY)
AMDF
[SSE, varexpl, fin_iters, time_elapsed, diagsum_final]
Fast Archetypal Analysis:
Compute the compositions when the archetypes are already given
|--------|--------------|--------------|-------------------------|
|   Iter |        SSE_i |    SSE_(i+1) | |SSE_(i+1)-SSE_i|/SSE_i |
|--------|--------------|--------------|-------------------------|
|      1 | 2.626019e+01 | 2.078703e+00 |                11.632968|
|      2 | 2.078703e+00 | 8.176473e-01 |                 1.542298|
|      3 | 8.176473e-01 | 1.286832e+00 |                 0.364605|
|      4 | 8.176473e-01 | 1.563447e-01 |                 4.229772|
|      5 | 1.563447e-01 | 1.204240e-01 |                 0.298286|
|      6 | 1.204240e-01 | 1.948338e-01 |                 0.381914|
|      7 | 1.204240e-01 | 1.339817e-02 |                 7.988091|
|      8 | 1.339817e-02 | 6.356475e-03 |                 1.107799|
|--------|--------------|--------------|-------------------------|
Time for the 8 A updates was 0 secs
|----------|------------|--------------|-------------------|--------------|
|     Iter |    VarExpl |          SSE | SSE_8 / SSE_0    |        muA   |
|----------|------------|--------------|-------------------|--------------|
|        8 |   0.999903 | 6.356475e-03 |          0.000242 |    7.4650e-01|
|----------|------------|--------------|-------------------|--------------|
The sum of diagonal elements for the sub-matrix of closer grid points is 4.0
The ideal sum would be 4
#closer_grid_archetypal(
BY, A, B, ADF, imins, SSE, varexpl, fin_iters, time_elapsed, diagsum_final = (
    closer_grid_archetypal(df,  diag_less = 1e-6, verbose = True))
pd.DataFrame(BY)
ADF
[SSE, varexpl, fin_iters, time_elapsed, diagsum_final]
Fast Archetypal Analysis:
Compute the compositions when the archetypes are already given
|--------|--------------|--------------|-------------------------|
|   Iter |        SSE_i |    SSE_(i+1) | |SSE_(i+1)-SSE_i|/SSE_i |
|--------|--------------|--------------|-------------------------|
|      1 | 2.339832e+01 | 2.111296e+00 |                10.082445|
|      2 | 2.111296e+00 | 5.136190e-01 |                 3.110626|
|      3 | 5.136190e-01 | 6.213599e-01 |                 0.173395|
|      4 | 5.136190e-01 | 1.098227e-01 |                 3.676804|
|      5 | 1.098227e-01 | 6.322219e-02 |                 0.737090|
|      6 | 6.322219e-02 | 8.338054e-02 |                 0.241763|
|      7 | 6.322219e-02 | 1.851679e-02 |                 2.414316|
|      8 | 1.851679e-02 | 1.440165e-02 |                 0.285741|
|      9 | 1.440165e-02 | 1.325812e-02 |                 0.086251|
|     10 | 1.325812e-02 | 1.334901e-02 |                 0.006809|
|     11 | 1.325812e-02 | 1.243129e-02 |                 0.066512|
|--------|--------------|--------------|-------------------------|
Time for the 11 A updates was 0 secs
|----------|------------|--------------|-------------------|--------------|
|     Iter |    VarExpl |          SSE | SSE_11 / SSE_0    |        muA   |
|----------|------------|--------------|-------------------|--------------|
|       11 |   0.999799 | 1.243129e-02 |          0.000531 |    5.3748e-01|
|----------|------------|--------------|-------------------|--------------|
The sum of diagonal elements for the sub-matrix of closer grid points is 4.0
The ideal sum would be 4
# fast_archetypal(): we use the imins from closer_grid_archetypal() above
BY, A, B, irows, SSE, varexpl, fin_iters, time_elapsed, diagsum_final = (
    fast_archetypal(df, irows = imins, verbose = True, diag_less = 1e-6))
pd.DataFrame(BY)
[SSE,varexpl,fin_iters, time_elapsed, diagsum_final]
Fast Archetypal Analysis:
Compute the compositions when the archetypes are already given
|--------|--------------|--------------|-------------------------|
|   Iter |        SSE_i |    SSE_(i+1) | |SSE_(i+1)-SSE_i|/SSE_i |
|--------|--------------|--------------|-------------------------|
|      1 | 2.240585e+01 | 1.936972e+00 |                10.567465|
|      2 | 1.936972e+00 | 5.236400e-01 |                 2.699052|
|      3 | 5.236400e-01 | 5.861317e-01 |                 0.106617|
|      4 | 5.236400e-01 | 1.122365e-01 |                 3.665504|
|      5 | 1.122365e-01 | 7.476762e-02 |                 0.501138|
|      6 | 7.476762e-02 | 8.903380e-02 |                 0.160233|
|      7 | 7.476762e-02 | 1.994893e-02 |                 2.747951|
|      8 | 1.994893e-02 | 1.549558e-02 |                 0.287395|
|      9 | 1.549558e-02 | 1.457414e-02 |                 0.063225|
|--------|--------------|--------------|-------------------------|
Time for the 9 A updates was 0 secs
|----------|------------|--------------|-------------------|--------------|
|     Iter |    VarExpl |          SSE | SSE_9 / SSE_0    |        muA   |
|----------|------------|--------------|-------------------|--------------|
|        9 |   0.999764 | 1.457414e-02 |          0.000650 |    8.9580e-01|
|----------|------------|--------------|-------------------|--------------|
# archetypal_pcha()
BY, A, B, SSE, varexpl, BY0, converges, iterations, total_time = (
    archetypal_pcha(df, kappas = 3, conv_crit=1E-6, maxiter=2000, verbose=True))
pd.DataFrame(BY0)
pd.DataFrame(BY)
[SSE, varexpl, converges, iterations, total_time]
PCHA Archetypal Analysis:
Principal Convex Hull Analysis / Archetypal Analysis
The mumber of Archetypes will be kappas = 3
To stop algorithm press control C
|----------|------------|------------|-------------|------------|------------|------------|------------|
      Iter |    VarExpl |       SSE  | |dSSE|/SSE  |        muC |    mualpha |        muS |  Time(s)   
|----------|------------|------------|-------------|------------|------------|------------|------------|
|        1 |   0.969057 | 1.9137e+00 |  7.0437e-01 |  1.548e+00 |  1.000e+00 |  1.154e+00 |      0.004 | 
|        2 |   0.973296 | 1.6515e+00 |  1.5874e-01 |  2.396e+00 |  1.000e+00 |  8.929e-01 |      0.004 | 
|        3 |   0.974737 | 1.5623e+00 |  5.7068e-02 |  7.418e+00 |  1.000e+00 |  1.382e+00 |      0.003 | 
|        4 |   0.975468 | 1.5171e+00 |  2.9789e-02 |  1.148e+01 |  1.000e+00 |  1.070e+00 |      0.004 | 
|        5 |   0.975934 | 1.4883e+00 |  1.9357e-02 |  1.777e+01 |  1.000e+00 |  1.656e+00 |      0.003 | 
|        6 |   0.976253 | 1.4686e+00 |  1.3440e-02 |  1.376e+01 |  1.000e+00 |  1.282e+00 |      0.004 | 
|        7 |   0.976555 | 1.4499e+00 |  1.2862e-02 |  2.129e+01 |  1.000e+00 |  1.984e+00 |      0.002 | 
|        8 |   0.976821 | 1.4335e+00 |  1.1475e-02 |  3.296e+01 |  1.000e+00 |  1.535e+00 |      0.002 | 
|        9 |   0.977052 | 1.4192e+00 |  1.0097e-02 |  2.551e+01 |  1.000e+00 |  1.188e+00 |      0.002 | 
|       10 |   0.977240 | 1.4075e+00 |  8.2598e-03 |  1.975e+01 |  1.000e+00 |  9.197e-01 |      0.002 | 
|       11 |   0.977397 | 1.3978e+00 |  6.9319e-03 |  1.528e+01 |  1.000e+00 |  1.424e+00 |      0.002 | 
|       12 |   0.977546 | 1.3886e+00 |  6.6443e-03 |  5.914e+00 |  1.000e+00 |  2.204e+00 |      0.002 | 
|       13 |   0.977713 | 1.3783e+00 |  7.4633e-03 |  4.577e+00 |  1.000e+00 |  8.528e-01 |      0.002 | 
|       14 |   0.977873 | 1.3684e+00 |  7.2652e-03 |  7.085e+00 |  1.000e+00 |  1.320e+00 |      0.002 | 
|       15 |   0.978040 | 1.3581e+00 |  7.6022e-03 |  5.484e+00 |  1.000e+00 |  1.022e+00 |      0.002 | 
|       16 |   0.978221 | 1.3469e+00 |  8.2898e-03 |  4.244e+00 |  1.000e+00 |  1.582e+00 |      0.002 | 
|       17 |   0.978424 | 1.3344e+00 |  9.4027e-03 |  6.570e+00 |  1.000e+00 |  1.224e+00 |      0.002 | 
|       18 |   0.978628 | 1.3217e+00 |  9.5674e-03 |  5.085e+00 |  1.000e+00 |  9.474e-01 |      0.002 | 
|       19 |   0.978841 | 1.3086e+00 |  1.0053e-02 |  3.935e+00 |  1.000e+00 |  1.467e+00 |      0.002 | 
|       20 |   0.979046 | 1.2959e+00 |  9.7856e-03 |  6.092e+00 |  1.000e+00 |  5.675e-01 |      0.002 | 
|       21 |   0.979247 | 1.2835e+00 |  9.6734e-03 |  4.715e+00 |  1.000e+00 |  8.785e-01 |      0.002 | 
|       22 |   0.979447 | 1.2710e+00 |  9.7607e-03 |  7.298e+00 |  1.000e+00 |  1.360e+00 |      0.002 | 
|       23 |   0.979640 | 1.2592e+00 |  9.4451e-03 |  5.649e+00 |  1.000e+00 |  1.052e+00 |      0.002 | 
|       24 |   0.979829 | 1.2474e+00 |  9.4144e-03 |  8.744e+00 |  1.000e+00 |  8.146e-01 |      0.002 | 
|       25 |   0.979933 | 1.2410e+00 |  5.1822e-03 |  6.767e+00 |  1.000e+00 |  1.261e+00 |      0.002 | 
|       26 |   0.980005 | 1.2366e+00 |  3.5570e-03 |  1.048e+01 |  1.000e+00 |  1.952e+00 |      0.002 | 
|       27 |   0.980053 | 1.2336e+00 |  2.4384e-03 |  1.622e+01 |  1.000e+00 |  7.553e-01 |      0.002 | 
|       28 |   0.980086 | 1.2315e+00 |  1.6616e-03 |  1.255e+01 |  1.000e+00 |  1.169e+00 |      0.002 | 
|       29 |   0.980109 | 1.2301e+00 |  1.1472e-03 |  1.943e+01 |  1.000e+00 |  9.049e-01 |      0.002 | 
|       30 |   0.980124 | 1.2292e+00 |  7.7082e-04 |  1.504e+01 |  1.000e+00 |  1.401e+00 |      0.002 | 
|       31 |   0.980135 | 1.2285e+00 |  5.2532e-04 |  2.327e+01 |  1.000e+00 |  1.084e+00 |      0.002 | 
|       32 |   0.980142 | 1.2281e+00 |  3.7454e-04 |  1.801e+01 |  1.000e+00 |  1.678e+00 |      0.002 | 
|       33 |   0.980147 | 1.2277e+00 |  2.5874e-04 |  1.394e+01 |  1.000e+00 |  1.299e+00 |      0.002 | 
|       34 |   0.980151 | 1.2275e+00 |  1.7650e-04 |  1.079e+01 |  1.000e+00 |  2.011e+00 |      0.002 | 
|       35 |   0.980154 | 1.2274e+00 |  1.2759e-04 |  1.670e+01 |  1.000e+00 |  1.556e+00 |      0.002 | 
|       36 |   0.980155 | 1.2273e+00 |  9.8252e-05 |  1.293e+01 |  1.000e+00 |  1.204e+00 |      0.002 | 
|       37 |   0.980157 | 1.2272e+00 |  7.7710e-05 |  1.001e+01 |  1.000e+00 |  9.321e-01 |      0.002 | 
|       38 |   0.980158 | 1.2271e+00 |  5.6505e-05 |  1.549e+01 |  1.000e+00 |  1.443e+00 |      0.002 | 
|       39 |   0.980159 | 1.2270e+00 |  4.9600e-05 |  1.199e+01 |  1.000e+00 |  1.117e+00 |      0.002 | 
|       40 |   0.980160 | 1.2270e+00 |  4.1790e-05 |  9.278e+00 |  1.000e+00 |  1.729e+00 |      0.002 | 
|       41 |   0.980161 | 1.2269e+00 |  3.7995e-05 |  1.436e+01 |  1.000e+00 |  1.338e+00 |      0.002 | 
|       42 |   0.980161 | 1.2269e+00 |  3.6791e-05 |  1.112e+01 |  1.000e+00 |  2.071e+00 |      0.002 | 
|       43 |   0.980162 | 1.2268e+00 |  3.3335e-05 |  1.721e+01 |  1.000e+00 |  1.603e+00 |      0.002 | 
|       44 |   0.980163 | 1.2268e+00 |  3.1141e-05 |  1.332e+01 |  1.000e+00 |  1.241e+00 |      0.002 | 
|       45 |   0.980163 | 1.2268e+00 |  3.3211e-05 |  1.031e+01 |  1.000e+00 |  9.602e-01 |      0.002 | 
|       46 |   0.980164 | 1.2267e+00 |  3.3546e-05 |  7.977e+00 |  1.000e+00 |  1.486e+00 |      0.002 | 
|       47 |   0.980165 | 1.2267e+00 |  3.1603e-05 |  1.235e+01 |  1.000e+00 |  1.150e+00 |      0.002 | 
|       48 |   0.980165 | 1.2266e+00 |  3.0910e-05 |  1.911e+01 |  1.000e+00 |  1.781e+00 |      0.002 | 
|       49 |   0.980166 | 1.2266e+00 |  3.1031e-05 |  1.479e+01 |  1.000e+00 |  1.378e+00 |      0.002 | 
|       50 |   0.980167 | 1.2266e+00 |  3.1274e-05 |  1.145e+01 |  1.000e+00 |  1.067e+00 |      0.002 | 
|       51 |   0.980167 | 1.2265e+00 |  3.0282e-05 |  1.772e+01 |  1.000e+00 |  1.651e+00 |      0.002 | 
|       52 |   0.980168 | 1.2265e+00 |  3.0849e-05 |  1.372e+01 |  1.000e+00 |  1.278e+00 |      0.002 | 
|       53 |   0.980168 | 1.2265e+00 |  3.1283e-05 |  1.062e+01 |  1.000e+00 |  9.890e-01 |      0.002 | 
|       54 |   0.980169 | 1.2264e+00 |  3.0494e-05 |  1.643e+01 |  1.000e+00 |  1.531e+00 |      0.002 | 
|       55 |   0.980170 | 1.2264e+00 |  3.1566e-05 |  1.272e+01 |  1.000e+00 |  1.185e+00 |      0.002 | 
|       56 |   0.980170 | 1.2263e+00 |  3.0652e-05 |  9.844e+00 |  1.000e+00 |  1.834e+00 |      0.002 | 
|       57 |   0.980171 | 1.2263e+00 |  2.6192e-05 |  3.048e+01 |  1.000e+00 |  1.420e+00 |      0.002 | 
|       58 |   0.980171 | 1.2263e+00 |  1.1450e-05 |  2.359e+01 |  1.000e+00 |  1.099e+00 |      0.002 | 
|       59 |   0.980171 | 1.2263e+00 |  9.3466e-06 |  1.826e+01 |  1.000e+00 |  1.701e+00 |      0.002 | 
|       60 |   0.980171 | 1.2263e+00 |  8.4407e-06 |  2.826e+01 |  1.000e+00 |  1.316e+00 |      0.002 | 
|       61 |   0.980171 | 1.2263e+00 |  8.4114e-06 |  2.187e+01 |  1.000e+00 |  1.019e+00 |      0.002 | 
|       62 |   0.980172 | 1.2263e+00 |  9.1324e-06 |  1.693e+01 |  1.000e+00 |  1.577e+00 |      0.002 | 
|       63 |   0.980172 | 1.2262e+00 |  8.8070e-06 |  1.310e+01 |  1.000e+00 |  1.221e+00 |      0.002 | 
|       64 |   0.980172 | 1.2262e+00 |  8.6021e-06 |  2.028e+01 |  1.000e+00 |  9.447e-01 |      0.002 | 
|       65 |   0.980172 | 1.2262e+00 |  8.4549e-06 |  1.570e+01 |  1.000e+00 |  1.462e+00 |      0.002 | 
|       66 |   0.980172 | 1.2262e+00 |  8.9234e-06 |  1.215e+01 |  1.000e+00 |  1.132e+00 |      0.002 | 
|       67 |   0.980172 | 1.2262e+00 |  8.7704e-06 |  1.881e+01 |  1.000e+00 |  8.759e-01 |      0.002 | 
|       68 |   0.980173 | 1.2262e+00 |  8.6715e-06 |  1.455e+01 |  1.000e+00 |  1.356e+00 |      0.002 | 
|       69 |   0.980173 | 1.2262e+00 |  8.0681e-06 |  2.253e+01 |  1.000e+00 |  1.049e+00 |      0.002 | 
|       70 |   0.980173 | 1.2262e+00 |  8.8384e-06 |  1.744e+01 |  1.000e+00 |  1.624e+00 |      0.002 | 
|       71 |   0.980173 | 1.2262e+00 |  8.6672e-06 |  2.699e+01 |  1.000e+00 |  1.257e+00 |      0.002 | 
|       72 |   0.980173 | 1.2261e+00 |  8.1818e-06 |  2.089e+01 |  1.000e+00 |  9.731e-01 |      0.002 | 
|       73 |   0.980174 | 1.2261e+00 |  8.9279e-06 |  1.617e+01 |  1.000e+00 |  1.506e+00 |      0.002 | 
|       74 |   0.980174 | 1.2261e+00 |  8.5495e-06 |  2.503e+01 |  1.000e+00 |  1.166e+00 |      0.002 | 
|       75 |   0.980174 | 1.2261e+00 |  8.5998e-06 |  1.937e+01 |  1.000e+00 |  9.023e-01 |      0.002 | 
|       76 |   0.980174 | 1.2261e+00 |  8.6971e-06 |  1.499e+01 |  1.000e+00 |  1.397e+00 |      0.002 | 
|       77 |   0.980174 | 1.2261e+00 |  8.5365e-06 |  2.321e+01 |  1.000e+00 |  1.081e+00 |      0.002 | 
|       78 |   0.980174 | 1.2261e+00 |  8.5858e-06 |  1.796e+01 |  1.000e+00 |  1.673e+00 |      0.002 | 
|       79 |   0.980175 | 1.2261e+00 |  8.4775e-06 |  2.780e+01 |  1.000e+00 |  1.295e+00 |      0.002 | 
|       80 |   0.980175 | 1.2261e+00 |  8.5313e-06 |  2.152e+01 |  1.000e+00 |  1.002e+00 |      0.002 | 
|       81 |   0.980175 | 1.2261e+00 |  8.6361e-06 |  1.665e+01 |  1.000e+00 |  1.552e+00 |      0.002 | 
|       82 |   0.980175 | 1.2260e+00 |  8.1931e-06 |  2.578e+01 |  1.000e+00 |  1.201e+00 |      0.002 | 
|       83 |   0.980175 | 1.2260e+00 |  8.6973e-06 |  1.995e+01 |  1.000e+00 |  9.294e-01 |      0.002 | 
|       84 |   0.980175 | 1.2260e+00 |  8.5786e-06 |  1.544e+01 |  1.000e+00 |  1.439e+00 |      0.002 | 
|       85 |   0.980176 | 1.2260e+00 |  8.3171e-06 |  2.391e+01 |  1.000e+00 |  1.114e+00 |      0.002 | 
|       86 |   0.980176 | 1.2260e+00 |  8.7468e-06 |  1.850e+01 |  1.000e+00 |  8.618e-01 |      0.002 | 
|       87 |   0.980176 | 1.2260e+00 |  8.7327e-06 |  1.432e+01 |  1.000e+00 |  1.334e+00 |      0.002 | 
|       88 |   0.980176 | 1.2260e+00 |  8.2775e-06 |  2.217e+01 |  1.000e+00 |  1.032e+00 |      0.002 | 
|       89 |   0.980176 | 1.2260e+00 |  8.7811e-06 |  1.716e+01 |  1.000e+00 |  1.598e+00 |      0.002 | 
|       90 |   0.980176 | 1.2260e+00 |  8.6705e-06 |  1.328e+01 |  1.000e+00 |  2.474e+00 |      0.002 | 
|       91 |   0.980177 | 1.2259e+00 |  8.4991e-06 |  2.055e+01 |  1.000e+00 |  9.574e-01 |      0.002 | 
|       92 |   0.980177 | 1.2259e+00 |  8.6603e-06 |  1.591e+01 |  1.000e+00 |  1.482e+00 |      0.002 | 
|       93 |   0.980177 | 1.2259e+00 |  8.0501e-06 |  2.462e+01 |  1.000e+00 |  1.147e+00 |      0.002 | 
|       94 |   0.980177 | 1.2259e+00 |  8.5048e-06 |  1.906e+01 |  1.000e+00 |  8.877e-01 |      0.002 | 
|       95 |   0.980177 | 1.2259e+00 |  8.3868e-06 |  2.950e+01 |  1.000e+00 |  1.374e+00 |      0.002 | 
|       96 |   0.980177 | 1.2259e+00 |  9.5861e-06 |  1.142e+01 |  1.000e+00 |  2.127e+00 |      0.002 | 
|       97 |   0.980178 | 1.2259e+00 |  8.7613e-06 |  1.767e+01 |  1.000e+00 |  1.646e+00 |      0.002 | 
|       98 |   0.980178 | 1.2259e+00 |  8.9700e-06 |  1.368e+01 |  1.000e+00 |  1.274e+00 |      0.002 | 
|       99 |   0.980178 | 1.2259e+00 |  7.8132e-06 |  2.117e+01 |  1.000e+00 |  1.972e+00 |      0.002 | 
|      100 |   0.980178 | 1.2259e+00 |  9.5240e-06 |  1.639e+01 |  1.000e+00 |  1.527e+00 |      0.002 | 
|----------|------------|------------|-------------|------------|------------|------------|------------|
      Iter |    VarExpl |       SSE  | |dSSE|/SSE  |        muC |    mualpha |        muS |  Time(s)   
|----------|------------|------------|-------------|------------|------------|------------|------------|
|      101 |   0.980178 | 1.2258e+00 |  8.5607e-06 |  2.536e+01 |  1.000e+00 |  1.181e+00 |      0.002 | 
|      102 |   0.980178 | 1.2258e+00 |  8.7858e-06 |  1.963e+01 |  1.000e+00 |  1.829e+00 |      0.002 | 
|      103 |   0.980179 | 1.2258e+00 |  8.7585e-06 |  1.519e+01 |  1.000e+00 |  1.415e+00 |      0.002 | 
|      104 |   0.980179 | 1.2258e+00 |  8.6764e-06 |  2.352e+01 |  1.000e+00 |  2.191e+00 |      0.002 | 
|      105 |   0.980179 | 1.2258e+00 |  9.0183e-06 |  1.820e+01 |  1.000e+00 |  1.696e+00 |      0.002 | 
|      106 |   0.980179 | 1.2258e+00 |  8.8824e-06 |  1.409e+01 |  1.000e+00 |  1.313e+00 |      0.002 | 
|      107 |   0.980179 | 1.2258e+00 |  8.6711e-06 |  2.181e+01 |  1.000e+00 |  1.016e+00 |      0.002 | 
|      108 |   0.980180 | 1.2258e+00 |  8.7784e-06 |  1.688e+01 |  1.000e+00 |  1.572e+00 |      0.002 | 
|      109 |   0.980180 | 1.2258e+00 |  8.8722e-06 |  1.306e+01 |  1.000e+00 |  2.434e+00 |      0.002 | 
|      110 |   0.980180 | 1.2257e+00 |  8.7731e-06 |  2.022e+01 |  1.000e+00 |  9.419e-01 |      0.002 | 
|      111 |   0.980180 | 1.2257e+00 |  8.7979e-06 |  1.565e+01 |  1.000e+00 |  1.458e+00 |      0.002 | 
|      112 |   0.980180 | 1.2257e+00 |  8.4729e-06 |  2.423e+01 |  1.000e+00 |  1.128e+00 |      0.002 | 
|      113 |   0.980180 | 1.2257e+00 |  8.9500e-06 |  1.875e+01 |  1.000e+00 |  8.734e-01 |      0.002 | 
|      114 |   0.980181 | 1.2257e+00 |  8.9462e-06 |  1.451e+01 |  1.000e+00 |  1.352e+00 |      0.002 | 
|      115 |   0.980181 | 1.2257e+00 |  8.9787e-06 |  2.246e+01 |  1.000e+00 |  2.093e+00 |      0.002 | 
|      116 |   0.980181 | 1.2257e+00 |  8.9491e-06 |  1.739e+01 |  1.000e+00 |  1.620e+00 |      0.002 | 
|      117 |   0.980181 | 1.2257e+00 |  8.9754e-06 |  1.346e+01 |  1.000e+00 |  1.254e+00 |      0.002 | 
|      118 |   0.980181 | 1.2257e+00 |  8.8896e-06 |  2.083e+01 |  1.000e+00 |  9.703e-01 |      0.002 | 
|      119 |   0.980181 | 1.2256e+00 |  8.8829e-06 |  1.612e+01 |  1.000e+00 |  1.502e+00 |      0.002 | 
|      120 |   0.980182 | 1.2256e+00 |  9.2186e-06 |  1.248e+01 |  1.000e+00 |  1.162e+00 |      0.002 | 
|      121 |   0.980182 | 1.2256e+00 |  8.8778e-06 |  1.931e+01 |  1.000e+00 |  1.799e+00 |      0.002 | 
|      122 |   0.980182 | 1.2256e+00 |  9.2538e-06 |  1.495e+01 |  1.000e+00 |  1.393e+00 |      0.002 | 
|      123 |   0.980182 | 1.2256e+00 |  9.0276e-06 |  2.314e+01 |  1.000e+00 |  1.078e+00 |      0.002 | 
|      124 |   0.980182 | 1.2256e+00 |  9.1088e-06 |  1.791e+01 |  1.000e+00 |  1.668e+00 |      0.002 | 
|      125 |   0.980183 | 1.2256e+00 |  9.0611e-06 |  2.772e+01 |  1.000e+00 |  1.291e+00 |      0.002 | 
|      126 |   0.980183 | 1.2256e+00 |  9.1043e-06 |  2.146e+01 |  1.000e+00 |  9.995e-01 |      0.002 | 
|      127 |   0.980183 | 1.2256e+00 |  2.6405e-06 |  1.661e+01 |  1.000e+00 |  1.547e+00 |      0.002 | 
|      128 |   0.980183 | 1.2256e+00 |  9.1533e-07 |  2.571e+01 |  1.000e+00 |  2.395e+00 |      0.001 | 
|----------|------------|------------|-------------|------------|------------|------------|------------|
|      128 |   0.980183 | 1.2256e+00 |  9.1533e-07 |  2.571e+01 |  1.000e+00 |  2.395e+00 |      0.001 | 
|----------|------------|------------|-------------|------------|------------|------------|------------|

```


Contact
-------

Please send comments, suggestions or bug reports to
<dchristop@econ.uoa.gr> or <dem.christop@gmail.com>

GitHub repository:

https://github.com/dchristop/geom_archetypal

https://github.com/dchristop/geom_archetypal/issues
