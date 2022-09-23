# Overiew

Our developer community is full of industry professionals who want to integrate Matterport into their every-day workflows. We're committed to face this challenge, and that starts with opening up our API to architects, engineers, and any other [professionals who want to dive deeper into our platform](https://matterport.com/platform/developers).&#x20;

We offer a developer toolset that allows developers to directly connect to Matterport's back-end datastore, while also allowing customers to act on their models programmatically. From directly accessing data, to modifying content, to managing a model's status, to purchasing value-added services, we want our developers to have full control.

### Documentation  <a href="#documentation" id="documentation"></a>

You can learn more about our current GraphQL API capabilities in our [reference guide](https://api.matterport.com/docs/reference). This also grants you access to our interactive console, where you can experiment with the GraphQL API on a limited basis.&#x20;

To access the interactive console, you need to be logged into Matterport Cloud (my.matterport.com) with administrator credentials. \
\
[Learn more about constructing GraphQL queries and mutations](https://graphql.org/learn/queries/).

### Generate API Keys <a href="#generate-api-keys" id="generate-api-keys"></a>

1. Go to Matterport Cloud (my.matterport.com).
2. Click Settings in the lower left.
3. Select Developer Tools.
4. Go to the API Token Management section.&#x20;
   * Here, you can request and revoke API keys.&#x20;

You need to generate an API key that allows you to connect to our API endpoints. You can generate up to five keys for use across the different applications you want to build. When you create a new key, you are presented with the following:&#x20;

* Token Secret&#x20;
  * This is presented only once, so make sure to copy and save it securely.&#x20;
* Token ID&#x20;
  * This appears on the settings page.

API keys are "admin" or "all-access" keys. This means they grant users administrative credentials to the customer account. Using the API with the generated API key, developers can perform all administrative functions using the API, including archiving models and purchasing floorplans and MatterPaks. It's important to remember this when sharing your API keys. We strongly advise that you don't share your API keys with third-party companies or developers.

Note that accounts have only Sandbox mode enabled by default. For more information about Sandbox Mode, refer to the [Developer Tools Availability and Pricing](https://support.matterport.com/s/article/Developer-Tools-Pricing-and-Availability?language=en\_US) article.

### Connect to the Endpoints  <a href="#connect-to-the-endpoints" id="connect-to-the-endpoints"></a>

1. Access the API endpoints at:
   * Model API: [https://api.matterport.com/api/models/graph](https://api.matterport.com/api/models/graph).&#x20;
   * Account API: [https://api.matterport.com/api/accounts/graph](https://api.matterport.com/api/accounts/graph) (available only with Enterprise Subscription tiers)
2. Use the Token ID as the username.
3. Use the Token Secret as the password.
   * Example: _**Authorization: Basic \<base64\_encode(\<Token ID>:\<Token Secret)**_&#x20;

All standard http libraries should support this process, but make sure to set your preemptive authorization to "true".  &#x20;

For more information, refer to the [How do I connect and authenticate my API token?](https://support.matterport.com/s/article/API-FAQs?language=en\_US#authenticate) article.

### Error Codes  <a href="#error-codes" id="error-codes"></a>

All application-level errors have codes in their error extensions. Use the guide below to recognize and troubleshoot common error codes.&#x20;

#### &#x20;  1. request.unauthenticated&#x20;

No authorization token is present, or the authorization token has expired.&#x20;

#### &#x20;  2. request.unauthorized&#x20;

User attempted to access an operation or field that is not allowed.&#x20;

#### &#x20;  3. request.invalid&#x20;

The graph query could not be processed.&#x20;

#### &#x20;  4. error.internal&#x20;

The server was unable to process the request.&#x20;

#### &#x20;  5. not.found&#x20;

The requested object doesn't exist. You will see this error when using the specific ID field in the associated operation.&#x20;

#### &#x20;  6. not.unique&#x20;

An attempt was made to retrieve a single record from a secondary index, but multiple records matched the submitted query. This often happens when multiple models have the same internal ID.&#x20;

#### &#x20;  7. quota.exceeded&#x20;

Resource limited mutations. For example, attempting to activate more models than allowed due to subscription limitations.&#x20;

### Code Snippet Examples  <a href="#code-snippet-examples" id="code-snippet-examples"></a>

To get started, refer to [these code snippet examples](https://support.matterport.com/s/article/Model-API-Code-Snippets?language=en\_US).&#x20;

### FAQs  <a href="#faqs" id="faqs"></a>

#### What is an API?&#x20;

API is short for "[application programming interface](https://en.wikipedia.org/wiki/Application\_programming\_interface)." This is a communications protocol between different parts of a computer program. The main intention of an API is to simplify the implementation and maintenance of software.&#x20;

Matterport APIs allow developers or customers to programmatically connect their systems or applications directly to the Matterport system in order to access and modify data.&#x20;

#### Matterport also offers an "SDK." What's the difference?&#x20;

Prior to the Matterport API beta, Matterport developers primarily utilized the Showcase SDK (software development kit). The API beta is a supplemental feature. Let's go over the differences below..&#x20;

**Showcase SDK**&#x20;

The Showcase SDK is a set of programming commands that can be used by developers to extend Showcase capabilities, even if the Showcase is directly imbedded on another site or platform. Think of it as a thin, invisible layer that sits on top of the Showcase iFrame, only __ on the developer page. With that in mind, the SDK affects the experience only on one developer page per use. As such, models that have been shared on multiple sites are affected only on the developer's page where the SDK has been applied.&#x20;

**API**

As opposed to the SDK, the API connects directly __ to the Matterport backend. This allows developers to perform a variety of commands, like searching, reading data, changing data, and placing orders. The Matterport API allows developers to programmatically perform actions that customers take on our site.&#x20;

#### What accounts can I access using the API?&#x20;

We recommend only using the API to access the customer's account and models. __ Keep in mind, the API token is essentially a set of administrative credentials, and provides full access to the account, even to make purchases via API.&#x20;

#### What APIs are currently available?

Matterport currently offers two APIs:

* Model API. These commands search, read, and change model data, including model details like the name and address of the space, sharing URLs, images, videos, position data, the OBJ mesh file, the point cloud file, panoramic imagery, position points, and Tags.
* Account API (available only with Enterprise subscription tiers). These commands include managing users, inviting, updating permissions, and managing SDK keys.

#### What do I need to be able to access the Account API?

You need to have a developer license on any of our Enterprise SaaS Tiers.

#### How do I get started?&#x20;

You'll need to request an API token. To do so:&#x20;

1. Go to Matterport Cloud (my.matterport.com).
2. Click Settings in the lower left.
3. Select Developer Tools.
4. Go to the API Token Management section.
   * Here, you can request and revoke API keys.&#x20;

#### More questions?&#x20;

Check out our extended [Model API FAQ](https://support.matterport.com/s/article/API-FAQs?language=en\_US).&#x20;
