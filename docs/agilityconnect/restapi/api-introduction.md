## Introduction

The Agility Connect API allows other programs or user interfaces to interact with the Agility Connect platform.
Since the API is based on REST principles, it's very easy to write interactions with the system.
You can use pretty much any HTTP client in any programming language to interact with the API.

### Required Knowledge

If you plan to interact with Agility Connect through the API, you should be familiar with the following:

* JSON and/or XML
* Web services and RESTful APIs
* HTTP requests
* One or more programming languages, such as Python, Ruby, Javascript, PHP, Perl, C#, or C++.

### Validating the API

Before getting started, you should verify access to the API.

To verify the API is available (and check the version):

```
http://hostname:8080/api/version
```

To see all commands supported by the API:

```
http://hostname:8080/api
```

### Authenticating

Each request to the API must be authenticated via an `Authorization` header.  Token authorization is recommended, but Basic authorication can be enabled by a system administrator
if desired.

A request URL should be in the following format:

`http://localhost:8080/api/list_tasks`

#### Using a Token

If Token authorization is used, the `Authorization` header should be as follows:

```
Authorization: Token <token>
```

Where the Token for a user is obtained by logging in to the Contiunuum UI and selecting `My Account` from the upper-right menu.

#### Using Basic

If the Administrator has enabled `Basic` authorization, the standard mechanism for HTTP Basic Auth is available:

```
Authorization: Basic <base64-encoded-creds>
```

Where `base64-encoded-creds` is the string `username:password` then Base64 encoded.

#### As an Argument

If it's not possible to set an `Authorization` header, an API request can be authenticated using a `token` querystring argument:

```
http://localhost:8080/api/list_tasks?token=12345
```

> This capability is the least secure and is provided as a convenience.  This capability may be deprecated in future releases.

### Obtaining a Token Programmatically

To get a token via the API, Basic Auth must be enabled, and a Basic Auth request must be issued to:

```
http://localhost:8080/api/get_token
```

The `get_token` function will respond with an API token, which can now be used for Token authorization.

### POSTing data

When using endpoints that require POST data, the data must be a JSON string, and the `Content-Type: application/json` header must be set.

### Common Arguments

Almost all API commands recognize several standard arguments.  All of these arguments are optional:

* `output_delimiter` - Delimiter for the "text" output format.  (Default is TAB)
* `header` - For the "text" output format, will omit the column header if 'false'.

### Output Formatting

The Agility Connect API can respond with three different formats - JSON, XML and Text.  If not specified, the default response is XML.
Response format can be changed by using an `Accept` header as follows:

#### Accept Header

```
Accept: application/json
```

The valid options are `application/json`, `application/xml` and `text/plain`.

#### As an Argument

If you cannot send an `Accept` header, the response format can be set using the `output_format` querystring option.

```
http://localhost:8080/api/list_tasks?output_format=text
```

If using the querystring option, the valid values are `xml`, `json`, and `text`.


### Immediate versus Eventual Results

In most cases, the results from an API call are timely and accurate.  However, when automation is involved, an API client will likely
need to implement a polling mechanism to check statuses, etc.

For example, the `list_tasks` command will immediately return a list of all Tasks.  There is no delay.

However, some API commands initiate a Pipeline, Task or other sequence of automation, the final results of which are never immediately available.

For example, the `initiate_pipeline` command will kick off a Pipeline, which could take a while to complete.  However, the `initiate_pipeline` command will _immediately_ return
with information about the Pipeline Run (status, identifier, etc).

In this case, a client should then use the identifier to occasionally issue another command, such as `get_pipelineinstance`, and check the progress of the Pipeline.
