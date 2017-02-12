# REST API (WIP)

Base URL for the API server is: https://api.keyvalue.xyz 

---
## POST /new/{key}

### Parameters
| Description | Limit     | Encoding | Notes                                                              |
|-------------|-----------|----------|--------------------------------------------------------------------|
| `{key}`     | 100 bytes | UTF-8    | Cannot contain: `. $ # [ ] /` ASCII control characters 0-31 or 127 |

### Response
| Code  | Body                                    | Notes                                  |
|-------|-----------------------------------------|----------------------------------------|
| `400` |                                         | Error occurred during new key creation                                       |
| `200` | `https://api.keyvalue/xyz/{token}/{key}` |  |


### Example
---
```
curl -X POST https://api.keyvalue.xyz/new/key
https://api.keyvalue.xyz/7d8cd2b1/key

curl -X POST -IL https://api.keyvalue.xyz/new/key.with.dot
HTTP/1.1 400 Bad Request
...
```
---
## POST /{token}/{key}/{value}

### Parameters

### Response

### Example
---

---
## GET /{token}/{key}

### Parameters

### Response

### Example
---
