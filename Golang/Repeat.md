- Repeat the function execution every hour
```
t := time.NewTicker(time.Hour)

for {
    functionToRepeat()
    <-t.C
}
```
