### Introduction
Sample implementation of containerized microservices with Nginx reverse proxy for service routing with built-in Docker DNS

### Steps
1. Setup development environment with ansible (Make sure that ansible hosts are configured properly)
   * ``` ansible-playbook ansible-docker.yml ```
2. Run containerised microservices with docker-compose (Make sure that specified ports and addresses are not already used)
   * ``` docker-compose up --build ```
3. Check HTTP router functionality with HTTP client
#### Authentication Service
  ```bash
      http --form post http://localhost/platform/authentication/token \
        username=alice \
        password=password
  ```
##### Request
```http
POST /platform/authentication/token HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 32
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Host: localhost
User-Agent: HTTPie/0.9.8

username=alice&password=password
```
##### Response
```http
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 191
Content-Type: application/json
Date: Sun, 25 Feb 2018 21:06:23 GMT
Server: nginx/1.13.9

{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxLCJ1c2VybmFtZSI6ImFsaWNlIiwiY2FuX3RyYW5zYWN0Ijp0cnVlLCJleHAiOjE1MTk1OTI4MTN9.zf_rx_A7USFOXBDuGUk9fhDMzEe6zcDaleqoh588wRc"
}
```
#### Transaction Service
  ```bash
      http -v --form post http://localhost/platform/transactions/transactions \
        amount=2000 \
        currency=GBP \
        token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxLCJ1c2VybmFtZSI6ImFsaWNlIiwiY2FuX3RyYW5zYWN0Ijp0cnVlLCJleHAiOjE1MTk1OTI4MTN9.zf_rx_A7USFOXBDuGUk9fhDMzEe6zcDaleqoh588wRc
  ```
##### Request
```http
POST /platform/transactions/transactions HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 204
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Host: localhost
User-Agent: HTTPie/0.9.8

amount=2000&currency=GBP&token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxLCJ1c2VybmFtZSI6ImFsaWNlIiwiY2FuX3RyYW5zYWN0Ijp0cnVlLCJleHAiOjE1MTk1OTI4MTN9.zf_rx_A7USFOXBDuGUk9fhDMzEe6zcDaleqoh588wRc
```
##### Response
```http
HTTP/1.1 200 OK
Connection: keep-alive
Content-Length: 60
Content-Type: application/json
Date: Sun, 25 Feb 2018 21:06:45 GMT
Server: nginx/1.13.9

{
    "amount": 2000,
    "currency": "GBP",
    "user_id": 1
}
```
[source]

[source]: https://github.com/yoyowallet/devops-interview
