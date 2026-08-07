<div align="center">

```
  equity
    │                                        ╭────────
    │                                ╭───────╯
    │                        ╭───────╯
    │              ╭──╮      │
    │        ╭─────╯  ╰──────╯   ← this part gets published too
    │   ╭────╯
    │───╯
    └──────────────────────────────────────────────▶  time
```

# QuantLodge

**Quant research lab — trading strategies, experiments and systematic edge.**

`no signals` · `no courses` · `no annual return in the repo description`

</div>

---

### What this is

A workshop. We build the boring parts nobody posts about: reference data that is
actually correct, backtests that survive contact with reality, and execution that
does not require a human staring at a screen.

Most trading repos show you the equity curve. We are more interested in the four
lines of code that decide whether that curve means anything.

### House rules

```
1. Backtest or it didn't happen.
2. If it only works in-sample, it doesn't work.
3. The drawdown is part of the track record, not a footnote.
4. Survivorship bias is not a rounding error — it's most of your alpha.
5. Reference data is a research problem, not a CSV you download once.
6. If you can't reproduce it from raw data, it's an anecdote.
```

### The one line that separates a strategy from a time machine

```python
# The backtest everybody posts
signal = df["close"] > df["close"].rolling(20).mean()
pnl    = signal * df["close"].pct_change().shift(-1)      # ← you just traded
                                                          #   on a close you
                                                          #   couldn't know yet

# The backtest that survives
signal = (df["close"] > df["close"].rolling(20).mean()).shift(1)
pnl    = signal * df["close"].pct_change()                # decided yesterday,
                                                          #   filled today
```

> Same idea, same data, one `.shift(1)` apart. The first version prints a
> gorgeous equity curve and loses money in production.
> A strategy that stops working once you fix this was never a strategy —
> it was a lookup of answers you already had.

### What's in the lodge

| Repo | What it is |
|---|---|
| [`ticker-reference-data`](https://github.com/Quant-Lodge/ticker-reference-data) | US ticker reference data, rebuilt daily. Splits the vendor missed, ticker renames resolved by CIK, and every trading halt since 2019. Published as dated releases so a backtest can pin the exact snapshot it used. |

More coming: backtesting harness, market data pipelines, execution tooling.

### Why reference data first

Because it is the least glamorous and most expensive mistake in the stack. Your
model is fine. Your universe is lying to you: the ticker that changed name in 2021,
the reverse split the vendor silently applied backwards, the halt that never made
it into your bars. Fix that layer and half your "alpha" disappears — which is the
point. What survives is real.

### Open to collaborators

Engineers who ship, traders with a documented edge, and anyone who has opinions
about point-in-time data. Open an issue, or come argue with us in the lodge.

<div align="center">

[![Discord](https://img.shields.io/badge/Discord-join%20the%20lodge-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/MHA5hFdWHS)

**It's a small room, on purpose.** No signal groups, no "what's your entry".
Data problems, backtest post-mortems and screenshots of things that broke.

---

**[Public trading track record →](https://jose.ar/journal)**

5,600+ trades. Curve, drawdown and profit factor. Updated daily, nothing hidden.

</div>

---

<div align="center">

```
        ┌───────────────────────────────────┐
        │  in backtests, everyone is rich.  │
        │  the lodge is about the rest.     │
        └───────────────────────────────────┘
```

<sub>Nothing here is financial advice. Past performance is a data point, not a promise.</sub>

</div>
