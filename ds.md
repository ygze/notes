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


## [Scalable Web Architecture and Distributed Systems](chrome-extension://ecabifbgmdmgdllomnfinbmaellmclnh/data/reader/index.html?id=108)

#### Principles of Web Distributed Systems Design

* **Availability**:

The uptime of a website is absolutely critical to the reputation and functionality of many companies. For some of the larger online retail sites, being unavailable for even minutes can result in thousands or millions of dollars in lost revenue, so designing their systems to be constantly available and resilient to failure is both a fundamental business and a technology requirement. High availability in distributed systems requires the careful consideration of redundancy for key components, rapid recovery in the event of partial system failures, and graceful degradation when problems occur.

* **Performance**:

Website performance has become an important consideration for most sites. The speed of a website affects usage and user satisfaction, as well as search engine rankings, a factor that directly correlates to revenue and retention. As a result, creating a system that is optimized for fast responses and low latency is key.
* **Reliability**:

A system needs to be reliable, such that a request for data will consistently return the same data. In the event the data changes or is updated, then that same request should return the new data. Users need to know that if something is written to the system, or stored, it will persist and can be relied on to be in place for future retrieval.
* **Scalability**:

When it comes to any large distributed system, size is just one aspect of scale that needs to be considered. Just as important is the effort required to increase capacity to handle greater amounts of load, commonly referred to as the scalability of the system. Scalability can refer to many different parameters of the system: how much additional traffic can it handle, how easy is it to add more storage capacity, or even how many more transactions can be processed.
* **Manageability**:

Designing a system that is easy to operate is another important consideration. The manageability of the system equates to the scalability of operations: maintenance and updates. Things to consider for manageability are the ease of diagnosing and understanding problems when they occur, ease of making updates or modifications, and how simple the system is to operate. (I.e., does it routinely operate without failure or exceptions?)
* **Cost**:

Cost is an important factor. This obviously can include hardware and software costs, but it is also important to consider other facets needed to deploy and maintain the system. The amount of developer time the system takes to build, the amount of operational effort required to run the system, and even the amount of training required should all be considered. Cost is the total cost of ownership.


There are challenges distributing data or functionality across multiple servers:
* data locality: in distributed systems the closer the data to the operation or point of computation, the better the performance of the system. Therefore it is potentially problematic to have data spread across multiple servers, as any time it is needed it may not be local, forcing the servers to perform a costly fetch of the required information across the network
* inconsistency: When there are different services reading and writing from a shared resource, potentially another service or data store, there is the chance for race conditions—where some data is supposed to be updated, but the read happens prior to the update—and in those cases the data is inconsistent.
* partitioning data

Options for making data access a lot faster:
* Caches:

Caches take advantage of the locality of reference principle: recently requested data is likely to be requested again. 
