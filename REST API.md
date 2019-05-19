# REST API (v1)

Base URL for the API server is: https://api.keyvalue.xyz 

| Method | Endpoint                  |
|--------|---------------------------|
| [POST](#post-newkey)   |  [`/new/{key}`](#post-newkey)             |
| [POST](#post-tokenkeyvalue)   |  [`/{token}/{key}`](#post-tokenkey) |
| [POST](#post-tokenkeyvalue)   |  [`/{token}/{key}/{value}`](#post-tokenkeyvalue) |
| [GET](#get-tokenkey)    | [`/{token}/{key}`](#get-tokenkey)           |
| [GET](#get-ping)    | [`/ping`](#get-ping)           |
| [GET](#get-timestamp)    | [`/timestamp`](#get-timestamp)           |

---

## POST `/new/{key}`

### Explanation
This API is used to create new `{key}` and if the request is successful it returns new `{token}` and `{key}`.

### Parameters
| Description | Limit     | Encoding | Notes                                                              |
|-------------|-----------|----------|--------------------------------------------------------------------|
| `{key}`     | 100 bytes | UTF-8    | Cannot contain: `. $ # [ ] /` ASCII control characters 0-31 or 127 |

### Response
| Code  | Body                                    | Notes                                  |
|-------|-----------------------------------------|----------------------------------------|
| `200` | `https://api.keyvalue.xyz/{token}/{key}` |  |
| `400` |                                         | Error occurred during new key creation                                       |

### Example
```
curl -X POST https://api.keyvalue.xyz/new/key
https://api.keyvalue.xyz/7d8cd2b1/key

curl -X POST -IL https://api.keyvalue.xyz/new/key.with.dot
HTTP/1.1 400 Bad Request
...
```
---

## POST `/{token}/{key}`

### Explanation
This API is used to set value for the `{key}` and if the request is successful `{value}` from the request body is stored.

### Parameters
| Description | Limit     | Encoding | Notes                                                              |
|-------------|-----------|----------|--------------------------------------------------------------------|
| `{token}`     | 100 bytes | UTF-8    | Cannot contain: `. $ # [ ] /` ASCII control characters 0-31 or 127 |
| `{key}`   | 100 bytes | UTF-8    | Cannot contain: `. $ # [ ] /` ASCII control characters 0-31 or 127 |
| `{value}`   | 1mb | UTF-8    | Send within the body of the request, could not be empty |

### Response
| Code  | Body                                    | Notes                                  |
|-------|-----------------------------------------|----------------------------------------|
| `200` |  | `{value}` is successfully saved   |
| `400` |  |                                       |

### Example
```
curl -X POST  https://api.keyvalue.xyz/3dc51064/key --data '{ Datacenter: dc1, Service: kvaas}'
HTTP/1.1 200 OK
...

curl -X POST -IL https://api.keyvalue.xyz/3dc51064/key/
HTTP/1.1 400 Bad Request
...

```
---

## POST `/{token}/{key}/{value}`

### Explanation
This API is used to set value for the `{key}` and if the request is successful `{value}` is stored.

### Parameters
| Description | Limit     | Encoding | Notes                                                              |
|-------------|-----------|----------|--------------------------------------------------------------------|
| `{token}`     | 100 bytes | UTF-8    | Cannot contain: `. $ # [ ] /` ASCII control characters 0-31 or 127 |
| `{key}`   | 100 bytes | UTF-8    | Cannot contain: `. $ # [ ] /` ASCII control characters 0-31 or 127 |
| `{value}`   | 1mb | UTF-8    | Cannot contain: `. $ # [ ] /` ASCII control characters 0-31 or 127 |

### Response
| Code  | Body                                    | Notes                                  |
|-------|-----------------------------------------|----------------------------------------|
| `200` |  | `{value}` is successfully saved   |
| `400` |  |                                       |

### Example
```
curl -X POST -IL https://api.keyvalue.xyz/7d8cd2b1/key/value
HTTP/1.1 200 OK
...

curl -X POST -IL https://api.keyvalue.xyz/7d8cd2b1/key/{test:value}
HTTP/1.1 200 OK
...

curl -X POST -IL  https://api.keyvalue.xyz/7d8cd2b1/key.with.dot/value
HTTP/1.1 400 Bad Request
...

```
---

## GET `/{token}/{key}`

### Explanation
This API is used to get the value for the `{key}`

### Parameters
| Description | Limit     | Encoding | Notes                                                              |
|-------------|-----------|----------|--------------------------------------------------------------------|
| `{token}`     | 100 bytes | UTF-8    | Cannot contain: `. $ # [ ] /` ASCII control characters 0-31 or 127 |
| `{key}`   | 100 bytes | UTF-8    | Cannot contain: `. $ # [ ] /` ASCII control characters 0-31 or 127 |

### Response
| Code  | Body                                    | Notes                                  |
|-------|-----------------------------------------|----------------------------------------|
| `200` |  `{value}` |   |
| `400` |  |                                       |

### Example
```
curl https://api.keyvalue.xyz/7d8cd2b1/key
value


curl -IL  https://api.keyvalue.xyz/7d8cd2b1/key.with.dot
HTTP/1.1 400 Bad Request
...

```
---


## GET `/ping`

### Explanation
This API is used to ping API server

### Response
| Code  | Body                                    | Notes                                  |
|-------|-----------------------------------------|----------------------------------------|
| `200` |  OK |   |

### Example
```
curl https://api.keyvalue.xyz/ping
OK
```
---

## GET `/timestamp`

### Explanation
This API is used to get timestamp

### Response
| Code  | Body                                    | Notes                                  |
|-------|-----------------------------------------|----------------------------------------|
| `200` |  UNIX timestamp |   |

### Example
```
curl https://api.keyvalue.xyz/timestamp
1545600234
```
---
