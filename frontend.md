### General Questions:
##### How would you optimize a website's assets/resources?
*Images:*
* Server the proper image size. (We can use css media query to acheive this) e.g.
```
@media only screen
and (min-device-width : 320px) 
and (max-device-width : 480px) {
    .header {
        background-image: url(../images/background_400x200.jpg);
    }
}
```
* Compression. We can use photoshop or other applications to compress the images.
* Sprites. Like twitter bootstrap's icon. e.g.
```
.icon-edit {
    background-image: url("../img/glyphicons-halflings-white.png");
    background-position: -96px -72px;
}
```
* Caching
* Prefetching, tells the browser that you will need some resources in the near future and it should
be downloaded now, in advance. For example:
```
<link rel="prefetch" href="/images/background.jpg">
```

