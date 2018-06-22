Distributed System

[High Performance Networking in Chrome](http://www.aosabook.org/en/posa/high-performance-networking-in-chrome.html)

assume the worst case scenario for a typical broadband connection
* 50 ms for DNS
* 80 ms for TCP handshake (one RTT)
* 160 ms for SSL handshake (two RTTs)
* 40 ms for request to server
* 100 ms for server processing
* 40 ms for response from the server

That’s 470 milliseconds for a single request.


Table 1.1 - User perception of latency
|Time|Impact|
|----------|---------|
|0 - 100 ms|	Instant|
|100 - 300 ms|	Small perceptible delay|
|300 - 1000 ms|	Machine is working|
|1 s+	|Mental context switch|
|10 s+	|I’ll come back later…|

provide visual feedback in under 250 ms to keep the user engaged



Table 1.3 - Network optimization techniques used by Chrome
|content               |  Explaination |
|----------------------|-----------------------------------------------------|
|DNS pre-resolve	     |Resolve hostnames ahead of time, to avoid DNS latency|
|TCP pre-connect	     |Connect to destination server ahead of time, to avoid TCP handshake latency|
|Resource prefetching |	Fetch critical resources on the page ahead of time, to accelerate rendering of the page|
|Page prerendering	   |Fetch the entire page with all of its resources ahead of time, to enable instant navigation when triggered by the user|

optimization in Chrome:
 * Optimizing the Cold-boot Experience:
   Chrome remembers the top ten most likely hostnames accessed by the user following the browser start. As the browser loads, Chrome can trigger a DNS prefetch for the likely destinations. Use chrome://dns to check it.
 * Optimizing Interactions with the Omnibox: Besides remembering the URLs of pages that the user visited in the past, Omnibox also offers full text search over your history, as well as a tight integration with the search engine of your choice. Chrome allows us to inspect this data by visiting chrome://predictors.
 * Optimizing Cache Performance: Chrome has two different implementations of the internal cache: one backed by local disk, and second which stores everything in memory.  The in-memory implementation is used for the Incognito browsing mode and is wiped clean whenever you close the window.  Internally the disk cache implements its own set of data structures, all of which are stored within a single cache folder for your profile.  To check the cache , use chrome://net-internals/#httpCache.
 *Optimizing DNS with Prefetching: the ability of Chrome to learn the topology of each site and then use this information to accelerate future visits. To inspect the subresource hostnames stored by Chrome, navigate to chrome://dns and search for any popular destination hostname for your profile. In addition to all of the internal signals, the owner of the site is also able to embed additional markup on their pages to request the browser to pre-resolve a hostname.
 * Optimizing TCP Connection Management with Pre-connect: speculatively pre-connect to the destination host and complete the TCP handshake before the user dispatches the request. To see the hosts for which a TCP pre-connect has been triggered, open a new tab and visit chrome://dns. chrome://net-internals#sockets for exploring the state of all the open sockets in Chrome.
 * Optimizing Resource Loading with Prefetch Hints: Chrome supports two such hints, which can be embedded in the markup of the page:

  <link rel="subresource" href="/javascript/myapp.js">
  <link rel="prefetch"    href="/images/big.jpeg">

  Subresource and prefetch look very similar, but have very different semantics. When a link resource specifies its relationship as “prefetch”, it is an indication to the browser that this resource might be needed in a future navigation. In other words, it is effectively a cross-page hint. By contrast, when a resource specifies the relationship as a “subresource”, it is an early indication to the browser that the resource will be used on a current page, and that it may want to dispatch the request before it encounters it later in the document.
 * Optimizing Resource Loading with Browser Prefreshing: Resource prefreshing is a great example of the workflow of every experimental optimization in Chrome.
 * Optimizing Navigation with Prerendering
