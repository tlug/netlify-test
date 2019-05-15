Netlify Content-Type Setting Tests
==================================

This demonstrates a bug in Netlify's setting of `Content-type`
headers: it may, depending on the combination of upper and lower case
used for the header name in the config file, send two `Content-type`
headers [which violates the HTTP standard][so 3241326].

In the `netlify.toml`, the content-type override is specified as
follows for each subdir here. The result is a comma-separated list
summarizing the `content-type` headers (Netlify always sends all
header names in lower case) that came back. (Tested 2019-05-16.)

    Subdir      Header Name     Result

    lower/      content-type    text/plain, text/html
    mixed/      Content-type    text/plain, text/html
    upper/      Content-Type    text/html

In the "lower" and "mixed" cases (pun intended!) we get back two
`content-type` headers, first what looks like an automatically
generated one and then the one we specified. Only in the "upper" case
did we get back just the `content-type` header with the contents we
specified in the config file.

Chrome seems to use the last `Content-type` header sent. Firefox
displays downloaded pages according to the second `Content-type` but
stores the first `Content-type` in the cache, thus causing the page to
be displayed as the wrong type the next time you go back to it.



<!-------------------------------------------------------------------->
[so 3241326]: https://stackoverflow.com/q/3241326/107294

