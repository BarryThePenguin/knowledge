# web performance lessons - jason stangroome [(twitter)](https://twitter.com/jstangroome)

Cache in the browser
 - cached requests in the browser are big wins for performance
 - cache-control headers and expires headers
 - static resources, logos etc
 - query strings - be mindful of key order
 - cache busting - timestamps
 - protocol relative urls - transition http --> https - eg login, cart, etc
 - prefer GET over POST - can't cache POST requests

Appropriate resources
 - scripts/stylesheets
   - concat and minify/compress
 - images
   - resolution (and in html)
   - strip metadata
   - sprite inline

scripts
 - script defer (third party)
 - page load vs quality user metrics
 - shared CDN vs on-domain - more requests

web server
 - dynamic pages not found
   - bots creating 404 pages blowing cache
 - server side session state
   - don' retain cookies so filling session-storage (bots)
 - database contention - when under pressure can you focus on primary goals?

HTTPS and HTTP/2
 - TLS is fast! shh...
 - Multiplexing - single connection! multiple files!
 - server push - anticipate other referenced resources
 - domain sharding

Content delivery network
 - cookies
 - vary: user-agent - distill into small amount of buckets and cache the result
 - cross-site request forgery

User specific content is the major problem
Serve pages with no user content allows it to be cached
Serve user info separately
