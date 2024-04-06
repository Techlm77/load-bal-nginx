This Nginx configuration file is used to manage multiple web and Node.js servers, handling SSL termination and proxying traffic to the appropriate backend servers based on the requested domain name.

Here's a breakdown of what each section does:

Nginx Web Servers:
        The first two server blocks are configured to serve regular HTTPS traffic (example.co.uk and joss.example.co.uk).
        They listen on port 443 (HTTPS) and handle SSL termination using SSL certificates obtained from Let's Encrypt.
        The location / block within each server block proxies the incoming requests to a backend web server running on 192.168.1.10 and 192.168.1.11, preserving the original host header and client IP address.

Node.js Servers:
        The next two server blocks are configured to handle WebSocket traffic for Node.js applications (chat.example.co.uk and stream.example.co.uk).
        They also listen on port 443 (HTTPS) and handle SSL termination using SSL certificates obtained from Let's Encrypt.
        The location / block within each server block proxies the WebSocket traffic to the respective backend Node.js servers running on 192.168.1.12:8443 and 192.168.1.13:8444.
        They are configured to upgrade the HTTP connection to WebSocket using the Upgrade and Connection headers.

HTTP to HTTPS Redirect:
        The last server block listens on port 80 (HTTP) and handles HTTP traffic for all specified domain names (example.co.uk, joss.example.co.uk, chat.example.co.uk, stream.example.co.uk).
        It returns a 301 redirect response to instruct the client's browser to use HTTPS for the requested URL (https://$host$request_uri).

Overall, this configuration ensures that all incoming HTTP and WebSocket traffic for the specified domain names are properly redirected to HTTPS and proxied to the appropriate backend servers based on the requested domain name.
