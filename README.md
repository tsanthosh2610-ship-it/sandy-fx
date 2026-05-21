//@version=6
indicator("Signal Master Simple", overlay=true)

// EMA
ema50 = ta.ema(close, 50)
ema200 = ta.ema(close, 200)

// RSI
rsi = ta.rsi(close, 14)

// MACD
[macdLine, signalLine, _] = ta.macd(close, 12, 26, 9)

// Conditions
buySignal = ema50 > ema200 and rsi > 55 and ta.crossover(macdLine, signalLine)

sellSignal = ema50 < ema200 and rsi < 45 and ta.crossunder(macdLine, signalLine)

// Plot EMAs
plot(ema50, color=color.green)
plot(ema200, color=color.red)

// Buy Signal
plotshape(
    buySignal,
    style=shape.labelup,
    location=location.belowbar,
    color=color.green,
    text="BUY"
)

// Sell Signal
plotshape(
    sellSignal,
    style=shape.labeldown,
    location=location.abovebar,
    color=color.red,
    text="SELL"
)

// Alerts
alertcondition(buySignal, title="BUY", message="BUY Signal")
alertcondition(sellSignal, title="SELL", message="SELL Signal")
