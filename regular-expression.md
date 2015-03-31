# Negative Look Behind
```
(?<!: )box[^;]+;
```
matches
```
box-shadow: 1px 2px 3px black; box-sizing: 100% 100%; box-align: center;
```
in
```
display: box; box-shadow: 1px 2px 3px black; box-sizing: 100% 100%; box-align: center;
```
