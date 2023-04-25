[[Frontend - What happens when you go to Google]]

---

DNS

-   Check the cache
-   Google.ca.
-   Root authority
    -   100 IP addresses hardcoded on browser/devices
-   Tells you where the CA root server is
-   CA root server tells you what google.ca IP address is
    -   One of Google's load balancers

Load balancer

-   Server that's setup to handle a ton of requests
-   Redirects those requests to web servers

TCP/QUIC handshake

-   Establish a connection with the google server via the load balancer
-   Syn syn ack
    -   With the load balancer
    -   Which already has sessions with a bunch of Google servers
-   Second handshake to establish TLS (HTTPS)
-   QUIC protocol does both handshakes at the same time
-   Every request will now have a cookie

HTTP GET request

-   Google sends us an HTML page
-   It might even be a cached page (on Google's end) if you're not logged in

Downloading/Reading the HTML page

-   See the Network tab in the browser
-   Chrome can stream HTML
    -   Read the HTML as it comes in
-   Reads the HTML
    -   Requests additional resources like the CSS and JS in the link and script tags
    -
