HTTP API
=======

HTTP/HTTPS API allows you to perform a HTTP requests.

Sending Requests
----------------

### request ###
```api:c++
int HTTP::request(const char *method, String url, const void *payload, String headers,
                  void *resp);
```

Performs a HTTP request. It returns HTTP status code or 0 on unexpected errors.
If `resp` is set, the response body is stored in `resp`. Other arguments are:

- `method`: The capitalized method name.
- `url`: The URL.
- `payload`: The request body or `nullptr`.
- headers is a request headers like `"Foo: bar\r\nBaz: 123"`.

__Example:__ Create a new folder in a WebDAV.
```example:c++
int status;

status = HTTP.request("MKCOL",
                      "https://example.com/webdav/chandler/NewFolder",
                      nullptr,
                      "");

if (status != 201)
    Logging.printlnf("server returned %d", status);
```


### get ###
```api:c++
int HTTP::get(String url, String headers, void *resp);
```

Performs a GET request. It returns HTTP status code or 0 on unexpected errors.
If `resp` is set, the response body is stored in `resp`. Other arguments are:

- `url`: The URL.
- `headers`: The request headers like `"Foo: bar\r\nBaz: 123"`.



### post ###
```api:c++
int HTTP::post(String url, const void *payload, String headers,
               void *resp);
```

Performs a POST request. It returns HTTP status code or 0 on unexpected errors.
If `resp` is set, the response body is stored in `resp`. Other arguments are:

- `url`: The URL.
- `payload`: The request body or `nullptr`.
- `headers`: The request headers like `"Foo: bar\r\nBaz: 123"`.

__Example:__ Post "Hello!" to Slack using [Incoming Webhook](https://api.slack.com/incoming-webhooks).
```example:c++
int status;
auto resp = new char[512];

status = HTTP.post("https://hooks.slack.com/services/XXX/YYY/ZZZ",
                   "payload={\"text\": \"Hello!\"}",
                   "Content-Type: application/x-www-form-urlencoded",
                   &resp);

if (String(resp) != "ok")
    Logging.errorlnf("Slack says: %s", status, resp);
```


### put ###
```api:c++
int HTTP::put(String url, const void *payload, String headers,
              void *resp);
```

Performs a PUT request. It returns HTTP status code or 0 on unexpected errors.
If `resp` is set, the response body is stored in `resp`. Other arguments are:

- `url`: The URL.
- `payload`: The request body or `nullptr`.
- `headers`: The request headers like `"Foo: bar\r\nBaz: 123"`.


### delete ###
```api:c++
int HTTP::delete(String url, String headers, void *resp);
```

Performs a DELETE request. It returns HTTP status code or 0 on unexpected errors.
If `resp` is set, the response body is stored in `resp`. Other arguments are:

- `url`: The URL.
- `headers`: The request headers like `"Foo: bar\r\nBaz: 123"`.
