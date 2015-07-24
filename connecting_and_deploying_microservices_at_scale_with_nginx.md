# Connecting and Deploying Microservices at Scale with nginx

# Intro to Microservices
- Individual applications/services
- Connected over HTTP
- Need strong interface contracts
- Dynamic scaling catered to each service
- Adding new services can be simpler

# Using nginx for Microservices
## Proxy and Scale
- proxy_pass
- CGI application servers
    - fastcgi_pass
    - uwsgi_pass
    - scgi_pass
- memcached_pass
- proxy_pass

# Containers?

# Nice Old Features
## A/B testing
`split_clients` can be used to send clients to different upstream paths based on different variables (IP addresses is an example) - can be split up into percentages

# Shiny New Features
Stream module - used to connect non-HTTP services
can be used for reverse proxy, load balancing, SSL offload/reencryption, additional security

# Bits of nginx Roadmap
