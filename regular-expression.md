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
start matching from **@**, and any character **.** 1 or more **+**, this will match to the end of the urls. Now we need to exclude the extensions. We use **?=** to look ahead, there must be a **.** and **[a-z]{2,4}** means any letter combinations between 2 and 4 letters.

## Non-capturing Groups
If we a regex like this:
```
box-(shadow|sizing)
```
this will not only match **box-shadow** and **box-sizing**, but also capture the matches within *()*, if don't want to capture the matches, we can use the Non-capturing Groups:
```
box-(?:shadow|sizing)
```
where **?:** means non-capturing group.

## Stripping Out an Anchor Tag's Attributes
We want to stripe out the href attribute in an anchor tag
```
<a href="http://tutsplus.com">Visit Our Site</a>
```
we can use something like this
```
/href=["']([^"]+)["']/g
```

## Matching email address
If we want to match legit email addresses in the following
```
rex@envato.com
notreal@email
je@jef-way.com
maemail.com
fake@fake.buygoods
joe@example.uk.com
rex-wang@gmail.com
```
We can use this regex
```
/^.+?@.+\.[a-z]{2,4}$/igm
```
**^** means from the beginning of the line(when m flag is on)<br/>
**.+?** means one or more of any character, and non greedy
**[a-z]{2,4}** means any characters(i flag is on) between 2 and 4 of numbers
**$** means end of line
