# Connecting to our APIs

How you write your query depends on the **HTTP method** and **content-type** you specify. Per the GraphQL spec, the request can be sent as either GET or POST.&#x20;

**If you send a GET request:**

The parameters must be properly escaped in the query string.&#x20;

**If you send a POST request:**&#x20;

This should include a [JSON-encoded body, illustrated in this article.](https://graphql.org/learn/serving-over-http/#http-methods-headers-and-body%20.)

**Use this URL in your GET and POST requests:**&#x20;

[https://api.matterport.com/api/models/graph](http://api.matterport.com/api/models/graph)

**Sample HTTP GET request (using the URL above):**&#x20;

```url
https://api.matterport.com/api/models/graph?query=query{%20models{%20totalResults%20results%20{%20id%20name%20created%20modified%20visibility%20}}}
```

Authorization: Basic \<api credentials>&#x20;

**Sample cURL request:**&#x20;

```bash
curl \
--user [apiKey]:[apiSecret] \
-v 'https://api.matterport.com/api/models/graph?query=\{models\{totalResults%20results\{id%20created%20modified%20visibility\}\}\}'
```

Notice the symbols above taken from the cURL request - these are escaping for bash. The cURL will not automatically URL encode whitespace, which is why the **%20** is added.&#x20;
