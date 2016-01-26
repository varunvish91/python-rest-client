# Introduction #

Within the Google app engine environment, you understandably cannot use network functions such as those provided by httplib.request, urllib.urlopen and so on, mainly due to how they proxy these requests.

Google provides a urlfetch class, which has a different API for use, just like the rest of the http libraries available.

The two wrapper classes, Connection and GAE\_Connection provide the same API, but the first is based on httplib2 and the second uses the urlfetch.

# Details #

Simply, use Connection when in a normal environment, and use GAE\_Connection when in the Google App engine environment. Once I work out a suitable technique to recognise the given environment, I hope this to be automatic.

## Example code ##

(From within a deployed google app engine app, hooking into Twitter.)
```
from gae_restful_lib import GAE_Connection as Connection

conn = Connection('http://twitter.com/statuses', username='twitterusername', password='pass')

# No Auth needed
public_timeline_rss = conn.request_get('/public_timeline.rss')

# Basic Auth needed, although Digest is handled in the same way.
friends_timeline = conn.request_get('/friends_timeline.xml')

```