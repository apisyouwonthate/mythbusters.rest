# Mythbusters.REST

With the relatively recent appearance of GraphQL and gRPC on the API scene, a lot of people have started sharing some Interesting Opinions™.

If you would like to know the technical differences between REST, gRPC and GraphQL, then [this article](https://blog.apisyouwonthate.com/understanding-rpc-rest-and-graphql-2f959aadebe7) can help highlight that.

If you would like to know when to use a specific paradigm over another, then [this article](https://blog.apisyouwonthate.com/picking-the-right-api-paradigm-d476f1a622e8) can help with that.

If you would like to read some nonsense about REST that people have posted in their "I like GraphQL/gRPC/other but I didn't really understand REST so now I'm going to moan about REST" articles, then please do read on!

- [ ] GraphQL is REST 2.0 (Well defined subset, missing HATEOAS and Cacheability)
- [ ] REST means you have huge responses (Sparse Fieldsets)
- [ ] Type Systems (Hi, JSON Schema exists + baton rouge meme)
- [ ] REST means over-fetching
  - Compound Documents for HTTP/1 (JSON:API, OData, HAL)
  - HTTP/2 https://blog.apisyouwonthate.com/optimizing-for-the-speed-of-light-b465da26415c & https://blog.apisyouwonthate.com/lets-stop-building-apis-around-a-network-hack-9a68f7e83dd2
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