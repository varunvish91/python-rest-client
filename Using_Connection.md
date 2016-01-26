# Introduction #

Basic usage patterns for the Connection wrapper.

# Details #

## Usage ##

```
from restful_lib import Connection

# Should also work with https protocols
base_url = "http://ora.ouls.ox.ac.uk:8080/fedora"

conn = Connection(base_url, username="fedoraAdmin", password="blahblah")
```
## Examples ##

1- A DELETE request on http://example.org/items/11232344
```
conn = Connection("http://example.org", username="XXX", password="XXX")

conn.request_delete('/items/11232344')
```

2- A GET request to /search, with parameter q = "Test", and request header "Accept: text/json"
```
conn.request_get("/search", args={'q':'Test'}, headers={'Accept':'text/json'})
```
3- A HEAD request on "/item" (using the full request method, rather than one of the convenience ones) - it is not recommended to use the direct method when using the GAE\_Connection class, due to method names being remapped to integers by urlfetch. Use request\_head instead.
```
conn.request("/item", method="HEAD")
```
## Method Responses ##

All the methods respond with a dictionary with two parts: a dictionary of the response headers (status, etc) and a text item, with key 'body'.

E.g.

>>> conn.request\_post("/upload", body=body)
{u'body': u'', u'headers': {'status': '204', 'content-length': '0', 'server': 'Bigfoot/11.572.26883', 'connection': 'close', 'cache-control': 'max-age=7200, must-revalidate', 'date': 'Wed, 14 May 2008 16:09:18 GMT', 'content-type': 'text/plain; charset=UTF-8'}}