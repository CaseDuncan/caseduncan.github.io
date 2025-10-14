First I fetched the challenge homepage with a simple GET to see what the app served:
```bash
curl -i http://54.72.82.22:8804/
```
-i tells curl to include HTTP response headers in the output. The server replied with a 200 OK and an HTML page for the “Proxy Trouble” app (a small Flask/Werkzeug page with a form). That confirmed the service was a web app that accepts input and returns fetched content the right surface for an SSRF-style challenge.

I then tried a few obvious paths directly these returned `404s`, which is also useful to know because it tells us those endpoints are not public:
```bash
curl -i http://54.72.82.22:8804/flag
curl -i http://54.72.82.22:8804/internal
curl -i http://54.72.82.22:8804/admin

```
Each of those returned HTTP/1.1 404 NOT FOUND and a default Werkzeug 404 page that told us the flag wasn’t exposed directly on the public host and pushed us toward trying SSRF probes.

To validate the proxy’s SSRF behavior and probe internal loopback, you POSTed the form to ask the proxy to fetch an internal IPv6 address, observing a connection error that proved the proxy actually opened connections and returned the backend exception text:
```python
curl -s -i -X POST -L --data-urlencode url=http://[::1]:5000/flag" http://54.72.82.22:8804/
```
`-s` makes curl silent except for output, -i includes headers, `-X POST` sets the method to POST, `-L` follows redirects, and `--data-urlencode "url=..." `sends the form field URL encoded exactly what the web form would do. The response body contained an error message like Error: HTTPConnectionPool(host='::1', port=5000): Max retries exceeded ... Connection refused, which was valuable because it proved the proxy attempted to connect to the requested host/port and returned the urllib3/requests exception. That allowed you to fingerprint reachability (connection refused means the host is reachable but no service listening; timeouts would indicate filtering).

I then ran dirsearch to enumerate public paths and discovered robots.txt, which hinted at an internal hostname:
```bash
dirsearch -u http://54.72.82.22:8804
```
dirsearch scanned common paths and reported a 200 for /robots.txt. To fetch that file directly and inspect its contents I used curl with verbose output:
```bash
curl -v http://54.72.82.22:8804/robots.txt
```
`-v `prints the request/response handshake and the response body; the body showed: