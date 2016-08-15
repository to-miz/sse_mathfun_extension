# sse_mathfun_extension

SSE2 implementations of sin, cos, exp, log, tan, cot, atan, atan2
The sin, cos, exp and log functions were written by Julien Pommier (see unmodified sse_mathfun.h).
The tan, cot, atan, atan2 are written by Tolga Mizrak.

sse_mathfun_extension.h serves as an extension to sse_mathfun.h, implementing tan, cot, atan and atan2.
It is written as an extension to sse_mathfun.h instead of modifying it, just because I didn't want
to maintain a modified version of the original library. This way switching to a newer version of the
original library won't be a hassle.

License: zlib (same as sse_mathfun.h)

Here are the benchmarks on my machine:
```
Results on a 3.30 GHz AMD FX-6100 Six-Core, compiled with Visual C++ Enterprise 2015 Update 3 (x64)
command line: cl.exe /W4 /DUSE_SSE2 /EHsc- /MD /GS- /Gy /fp:fast /Ox /Oy- /GL /Oi /O2 sse_mathfun_test.c

checking sines on [0*Pi, 1*Pi]
max deviation from sinf(x): 5.96046e-08 at 0.193304238313*Pi, max deviation from cephes_sin(x): 0
max deviation from cosf(x): 5.96046e-08 at 0.303994872157*Pi, max deviation from cephes_cos(x): 0
deviation of sin(x)^2+cos(x)^2-1: 1.78814e-07 (ref deviation is 1.19209e-07)
   ->> precision OK for the sin_ps / cos_ps / sincos_ps <<-

checking sines on [-1000*Pi, 1000*Pi]
max deviation from sinf(x): 5.96046e-08 at  338.694424873*Pi, max deviation from cephes_sin(x): 0
max deviation from cosf(x): 5.96046e-08 at  338.694424873*Pi, max deviation from cephes_cos(x): 0
deviation of sin(x)^2+cos(x)^2-1: 1.78814e-07 (ref deviation is 1.19209e-07)
   ->> precision OK for the sin_ps / cos_ps / sincos_ps <<-

checking exp/log [-60, 60]
max (relative) deviation from expf(x): 1.18944e-07 at -56.8358421326, max deviation from cephes_expf(x): 0
max (absolute) deviation from logf(x): 1.19209e-07 at -1.67546617985, max deviation from cephes_logf(x): 0
deviation of x - log(exp(x)): 1.19209e-07 (ref deviation is 5.96046e-08)
   ->> precision OK for the exp_ps / log_ps <<-

checking tan on [-0.25*Pi, 0.25*Pi]
max deviation from tanf(x): 1.19209e-07 at 0.250000006957*Pi, max deviation from cephes_tan(x): 5.96046e-08
   ->> precision OK for the tan_ps <<-

checking tan on [-0.49*Pi, 0.49*Pi]
max deviation from tanf(x): 3.8147e-06 at -0.490000009841*Pi, max deviation from cephes_tan(x): 9.53674e-07
   ->> precision OK for the tan_ps <<-

checking cot on [0.2*Pi, 0.7*Pi]
max deviation from cotf(x): 1.19209e-07 at 0.204303119606*Pi, max deviation from cephes_cot(x): 1.19209e-07
   ->> precision OK for the cot_ps <<-

checking cot on [0.01*Pi, 0.99*Pi]
max deviation from cotf(x): 3.8147e-06 at 0.987876517942*Pi, max deviation from cephes_cot(x): 9.53674e-07
   ->> precision OK for the cot_ps <<-

checking atan on [-10*Pi, 10*Pi]
max deviation from atanf(x): 1.19209e-07 at -9.39207109497*Pi, max deviation from cephes_atan(x): 1.19209e-07
   ->> precision OK for the atan_ps <<-

checking atan on [-10000*Pi, 10000*Pi]
max deviation from atanf(x): 1.19209e-07 at  -7350.3826719*Pi, max deviation from cephes_atan(x): 1.19209e-07
   ->> precision OK for the atan_ps <<-

checking atan2 on [-1*Pi, 1*Pi]
max deviation from atan2f(x): 2.38419e-07 at (0.797784384786*Pi, -0.913876806545*Pi), max deviation from cephes_atan2(x): 2.38419e-07
   ->> precision OK for the atan2_ps <<-

checking atan2 on [-10000*Pi, 10000*Pi]
max deviation from atan2f(x): 2.38419e-07 at ( 658.284195009*Pi, -2685.93394561*Pi), max deviation from cephes_atan2(x): 2.38419e-07
   ->> precision OK for the atan2_ps <<-

exp([        -1000,          -100,           100,          1000]) = [            0,             0, 2.4061436e+38, 2.4061436e+38]
exp([    -nan(ind),           inf,          -inf,           nan]) = [2.4061436e+38, 2.4061436e+38,             0, 2.4061436e+38]
log([            0,           -10,         1e+30, 1.0005271e-42]) = [         -nan,          -nan,     69.077553,    -87.336548]
log([    -nan(ind),           inf,          -inf,           nan]) = [   -87.336548,     88.722839,          -nan,    -87.336548]
sin([    -nan(ind),           inf,          -inf,           nan]) = [    -nan(ind),     -nan(ind),           nan,           nan]
cos([    -nan(ind),           inf,          -inf,           nan]) = [          nan,     -nan(ind),     -nan(ind),           nan]
sin([       -1e+30,       -100000,         1e+30,        100000]) = [          inf,  -0.035749275,          -inf,   0.035749275]
cos([       -1e+30,       -100000,         1e+30,        100000]) = [    -nan(ind),    -0.9993608,     -nan(ind),    -0.9993608]
benching                 sinf .. ->   16.3 millions of vector evaluations/second ->  40 cycles/value on a 2600MHz computer
benching                 cosf .. ->   15.8 millions of vector evaluations/second ->  41 cycles/value on a 2600MHz computer
benching                 expf .. ->   18.8 millions of vector evaluations/second ->  35 cycles/value on a 2600MHz computer
benching                 logf .. ->   17.8 millions of vector evaluations/second ->  36 cycles/value on a 2600MHz computer
benching                 tanf .. ->   13.8 millions of vector evaluations/second ->  47 cycles/value on a 2600MHz computer
benching                 cotf .. ->   12.2 millions of vector evaluations/second ->  53 cycles/value on a 2600MHz computer
benching                atanf .. ->   10.4 millions of vector evaluations/second ->  62 cycles/value on a 2600MHz computer
benching               atan2f .. ->    5.3 millions of vector evaluations/second -> 121 cycles/value on a 2600MHz computer
benching            atan2_ref .. ->   11.7 millions of vector evaluations/second ->  56 cycles/value on a 2600MHz computer
benching                sqrtf .. ->   69.5 millions of vector evaluations/second ->   9 cycles/value on a 2600MHz computer
benching               rsqrtf .. ->   70.2 millions of vector evaluations/second ->   9 cycles/value on a 2600MHz computer
benching          cephes_sinf .. ->   15.2 millions of vector evaluations/second ->  43 cycles/value on a 2600MHz computer
benching          cephes_cosf .. ->   16.6 millions of vector evaluations/second ->  39 cycles/value on a 2600MHz computer
benching          cephes_expf .. ->    2.9 millions of vector evaluations/second -> 220 cycles/value on a 2600MHz computer
benching          cephes_logf .. ->    3.4 millions of vector evaluations/second -> 186 cycles/value on a 2600MHz computer
benching               sin_ps .. ->   30.6 millions of vector evaluations/second ->  21 cycles/value on a 2600MHz computer
benching               cos_ps .. ->   31.1 millions of vector evaluations/second ->  21 cycles/value on a 2600MHz computer
benching            sincos_ps .. ->   30.9 millions of vector evaluations/second ->  21 cycles/value on a 2600MHz computer
benching               exp_ps .. ->   27.3 millions of vector evaluations/second ->  24 cycles/value on a 2600MHz computer
benching               log_ps .. ->   23.5 millions of vector evaluations/second ->  28 cycles/value on a 2600MHz computer
benching               tan_ps .. ->   22.2 millions of vector evaluations/second ->  29 cycles/value on a 2600MHz computer
benching               cot_ps .. ->   22.0 millions of vector evaluations/second ->  29 cycles/value on a 2600MHz computer
benching              atan_ps .. ->   31.1 millions of vector evaluations/second ->  21 cycles/value on a 2600MHz computer
benching             atan2_ps .. ->   24.1 millions of vector evaluations/second ->  27 cycles/value on a 2600MHz computer
benching              sqrt_ps .. ->   63.9 millions of vector evaluations/second ->  10 cycles/value on a 2600MHz computer
benching             rsqrt_ps .. ->   64.1 millions of vector evaluations/second ->  10 cycles/value on a 2600MHz computer
```

As you can see the sinf, cosf, expf, logf, tanf, atanf, atan2f and sqrtf implementations of the Visual C++ c library are pretty well optimized themselves, but using the simd versions still gives you at least a boost of 2x, with atan_ps and atan2_ps having the biggest gains.