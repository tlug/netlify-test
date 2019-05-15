Netlify Content-Type Setting Tests
==================================

This demonstrates a bug in Netlify's setting of `Content-type`
headers: it may, depending on the combination of upper and lower case
used for the header name in the config file, send two `Content-type`
headers [which violates the HTTP standard][so 3241326].

In the `netlify.toml`, the content-type override is specified as
follows for each subdir here:

    Subdir      Header Name     Result

    lower/      content-type
    mixed/      Content-type
    upper/      Content-Type


<!-------------------------------------------------------------------->
[so 3241326]: https://stackoverflow.com/q/3241326/107294

