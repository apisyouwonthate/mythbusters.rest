# Mythbusters.REST

With the relatively recent appearance of GraphQL and gRPC on the API scene, a lot of people have started sharing some Interesting Opinions™.

If you would like to know the technical differences between REST, gRPC and GraphQL, then [this article](https://blog.apisyouwonthate.com/understanding-rpc-rest-and-graphql-2f959aadebe7) can help highlight that.

If you would like to know when to use a specific paradigm over another, then [this article](https://blog.apisyouwonthate.com/picking-the-right-api-paradigm-d476f1a622e8) can help with that.

If you would like to read some nonsense about REST that people have posted in their "I like GraphQL/gRPC/other but I didn't really understand REST so now I'm going to moan about REST" articles, then please do read on!

- [ ] GraphQL is REST 2.0 (Well defined subset, missing HATEOAS and Cacheability)
- [ ] REST means you have huge responses (Sparse Fieldsets) - Matt
- [ ] REST has no notion of Type Systems (Hi, JSON Schema exists + baton rouge meme)
- [ ] Fetching X resources means X requests, means waiting X seconds
  - They assume serial is required, ignoring Async
  - https://philsturgeon.uk/php/2013/11/12/benchmarking-codswallop-nodejs-v-php/
  - Compound Documents for HTTP/1 (JSON:API, OData, HAL)
  - HTTP/2 is a thing https://blog.apisyouwonthate.com/optimizing-for-the-speed-of-light-b465da26415c
  - https://blog.apisyouwonthate.com/lets-stop-building-apis-around-a-network-hack-9a68f7e83dd2
  - also http network caching means a lot of this content can skip the "Content Download" portion
- [ ] REST means long polling for changes because it doesnt include subscriptions
  - Nah you can do subscriptions however you like
  - with WebSockets or web hooks, which are both useful for different scenarios
  - https://medium.com/@philsturgeon/no-youre-describing-polling-and-complaining-that-rest-doesn-t-teach-you-how-to-use-webhooks-56df4ca58c5f?source=responses---------10---------------------
- [ ] REST means URL versioning
  - Roy has said /v1 is RPC for a while, and evolution is a thing (see image)
  - https://blog.apisyouwonthate.com/api-evolution-for-rest-http-apis-b4296519e564
  - https://blog.apisyouwonthate.com/surviving-deprecations-to-resources-and-properties-on-other-apis-9711e7def610
- [ ] There are different levels of REST (no, maturity model means HATEOAS or RPC)
- [ ] Facebook dumped their RESTish API (nope Graph API is still RESTish)
- [ ] JSON is slow
  - some parsers are slow but some are fast https://twitter.com/kellabyte/status/1098447972809900037?s=12
- [ ] PUT / PATCH confuses developers
  - ok sure but they're both useful for different things and implementing two different types of "Edit" in RPC is always confusing. updateFoo becomes updateFooAndMissingMeansNull or updateOnlyChangeProvidedFields ugh what
  - https://blog.apisyouwonthate.com/put-vs-patch-vs-json-patch-208b3bfda7ac
- [ ] REST is outdated because HTTP hasnt evolved
  - There are a lot of new HTTP specifications and extensions to 7231, and HTTP/2 is wildly different
  - REST holds up nicely with modern requirements and HTTP/2)
- [ ] REST is only for CRUD
  - https://www.thoughtworks.com/insights/blog/rest-api-design-resource-modeling




# Articles

Once we have the FAQ/FUD content up, we can start tagging commonly referenced articles with those FUDs. We'll keep a list here until we get around to doing it. PR in your "favourites".

- [ ] medium.freecodecamp.org/rest-apis-are-rest-in-peace-apis-long-live-graphql-d412e559d8e4
- [ ] sitepoint.com/rest-2-0-graphql/
- [ ] www.howtographql.com/basics/1-graphql-is-the-better-rest/
- [ ] hackernoon.com/dive-into-graphql-part-i-whats-wrong-with-rest-709ebcb898dc#e286

That last one has a lot of odd stuff in it, and I talked to the author a bunch which actually makes for some good content.


> Yep, that’s 5 HTTP requests, 5 times the network latency, 5 times the battery drain. Over a 3G network, count at least 5 seconds for the list of tweets to show up on screen. That’s u...

iOS lets you make 5 concurrent HTTP connections, so this would actually only be 1 second. http://blog.lightstreamer.com/2013/01/on-ios-url-connection-parallelism-and.html

5x requests in serial is slower than 5 async requests.

> REST doesn’t have the notion of schema, a contract that describes exactly what a web service is supposed to return. Just like with standards above, the absence of schema leads to the...

REST does not care about it no, but JSON Schema exists and it’s a thing. A lot of people ignore it, and that winds me up, but it’s not a failure of REST.

https://blog.apisyouwonthate.com/guessing-api-contracts-ac1b7eaebced
