
### Expected Move

https://squeezemetrics.com/monitor/docs

> Movement in price is usually denominated in dollars, points, or percent. Movement in price is rarely, if ever, denominated in what really matters—the price change in relation to historical volatility, i.e., the price change relative to how much it usually moves.
>
> If two stocks, A and B, both move 5.00% tomorrow, that's not very useful information on its own. If we know, however, that Stock A has been moving 1.00% per day, on average; and Stock B has been moving 10.00% per day, on average; then we're able to place those percentage moves in context:
>
> * Stock A moved 5.00x its average expected move.
> * Stock B moved 0.50x its average expected move.
>
> Another way to express the multiple of the expected move is in "mean absolute deviation" (MAD). A 1.00x move is a 1 MAD move. A 5.00x move is a 5 MAD move. A 5 MAD move is big.

### Show move as percent change

TradingView Pine Script that shows the percent change in the stock:

![image](https://github.com/user-attachments/assets/3167c4e8-43dd-4ada-b37b-ff62b679ddfb)

![image](https://github.com/user-attachments/assets/36722f0f-d818-464b-9f71-f40727d8a374)

### Show move size (percent change size)

Now, instead of plotting the *percent change* (which can be negative) let's show the *percent change size*:

![image](https://github.com/user-attachments/assets/8debd7c5-9727-4d92-82eb-eff377148aa8)

![image](https://github.com/user-attachments/assets/5ce3533d-ad51-4887-b2fb-9bd22403688e)

### Show expected move size (as sma of move size)

Let's take the average of the expected move size over the last month (20 daily candles).

We'll do this using the simple moving average of the percent change size:

![image](https://github.com/user-attachments/assets/7d867540-8e3a-4131-afc9-5c7e2efd0490)

![image](https://github.com/user-attachments/assets/27ae16c1-d2c5-4384-a291-9cc478823905)

### Expected move multiple

```
indicator("My script")
import TradingView/ta/9

change_percent = ta.changePercent(close, close[1]) // move
change_percent_abs = math.abs(change_percent)      // move size

change_percent_abs_sma = ta.sma(change_percent_abs, 20) // expected move

expected_move_multiple = change_percent / change_percent_abs_sma

plot(series = expected_move_multiple, title = 'expected_move_multiple', style = plot.style_columns)
```

![image](https://github.com/user-attachments/assets/52e03a12-3c05-4868-9245-cad781358347)

### Expected move size multiple (with sma)

```
indicator("My script")
import TradingView/ta/9

change_percent = ta.changePercent(close, close[1]) // move
change_percent_abs = math.abs(change_percent)      // move size

change_percent_abs_sma = ta.sma(change_percent_abs, 20) // expected move

expected_move_multiple = change_percent / change_percent_abs_sma

plot(series = math.abs(expected_move_multiple), title = 'expected_move_multiple', style = plot.style_columns)

plot(series = ta.sma(math.abs(expected_move_multiple), 20), title = 'expected_move_multiple sma', color = color.yellow)
```

![image](https://github.com/user-attachments/assets/5e262fa6-a83d-4480-89ad-1e5a2210d154)
