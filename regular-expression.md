## Negative Look Behind
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

## Positive Look Ahead
If we want to match all the urls in email addresses, but not including extensions.
```
rex@envato.com
rex@gmail.ca
rex@envato.en
rex@envato.net
rex@envato.n
```
We can use positive look ahead
```
/@.+(?=\.[a-z]{2,4})/g
```
start matching from **@**, and any character **.** 1 or more **+**, this will match to the end of the urls. Now we need to exclude the extensions. We use **?=** to look ahead, there must be a **.** and **[a-z]{2,4}** means any letters between 2 and 4.
