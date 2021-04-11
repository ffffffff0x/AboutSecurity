## CORS

`curl --head -s 'http://example.com/api/v1/secret' -H 'Origin: http://evil.com'`

Check to see what the server responds with in the `Access-Control-Allow-Origin:` (if anything) and if so, check if `Access-Control-Allow-Credentials: true` is present.

`Origin: null`
