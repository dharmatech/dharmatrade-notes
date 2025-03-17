



```pine script
// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © dharmatech

//@version=6
indicator("SMA 5D INCL DECL", overlay = true, timeframe = 'D')

sma = ta.sma(close, 5)

line_color = sma > sma[1] ? color.green : color.red

plot(sma, color = line_color)
```
