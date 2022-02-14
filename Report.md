# Report

---

## Google API key leaked to Public

**Summarize**

I found a bunch of endpoints that is leaking you Google Api key.
I tested the key and found it is vulnerable to Geocode Api.

List of vulnerable endpoints
- xx.xx.xx.xx

Here is how you can find the key.

just go to https://xx.xx.xx.xx
now right click and view page source .

Ctrl + f , Search AIza

Exploit POC:
API key is vulnerable for Geocode API! Here is the PoC link which can be used directly via browser:
https://maps.googleapis.com/maps/api/geocode/json?latlng=40,30&key=xxxxxxxxxxxxxxx

**Impact**

that the Google Maps API key (which is by design easily retrievable from the .apk) was missing some restrictions. It then could be used by anyone to query the Google Static Map API, and possibly lead to financial damage.

costing companies extra money and in some cases DOS.
Identifies cost:
- Staticmap 			|| $2 per 1000 requests
- Streetview 			|| $7 per 1000 requests
- Embed (Basic)			|| Free
- Embed (Advanced)		|| Free
- Directions 			|| $5 per 1000 requests
- Directions (Advanced) 	|| $10 per 1000 requests
- Geocode 			|| $5 per 1000 requests
- Distance Matrix 		|| $5 per 1000 elements
- Distance Matrix (Advanced) 	|| $10 per 1000 elements
- Find Place From Text 		|| $17 per 1000 elements
- Autocomplete 			|| $2.83 per 1000 requests
- Autocomplete Per Session 	|| $17 per 1000 requests
- Elevation 			|| $5 per 1000 requests
- Timezone 			|| $5 per 1000 requests
- Geolocation 			|| $5 per 1000 requests
- Place Details 		|| $17 per 1000 requests
- Nearby Search-Places		|| $32 per 1000 requests
- Text Search-Places 		|| $32 per 1000 requests
- Places Photo 			|| $7 per 1000 requests
