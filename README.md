## Additional record response

HTTP/1.1 201 Created
Connection: close
Content-Type: application/json; charset=utf-8
Date: Sun, 05 Jul 2026 06:10:09 GMT
Server: Kestrel
Location: http://localhost:5039/Pizza/3
Transfer-Encoding: chunked

{
  "id": 3,
  "name": "Pepperoni",
  "isGlutenFree": false
}

## Get
HTTP/1.1 200 OK
Connection: close
Content-Type: application/json; charset=utf-8
Date: Sun, 05 Jul 2026 06:14:14 GMT
Server: Kestrel
Transfer-Encoding: chunked

[
  {
    "id": 1,
    "name": "Classic Italian",
    "isGlutenFree": false
  },
  {
    "id": 2,
    "name": "Veggie",
    "isGlutenFree": true
  },
  {
    "id": 3,
    "name": "Pepperoni",
    "isGlutenFree": false
  }
]
