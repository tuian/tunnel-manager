# Tunnel Manager

An RESTful API to control [pptp2http](https://github.com/bearice/pptp2http) instances

## API Endpoints

### `GET /tunnels`
 
Get list of tunnels
 
```
GET /tunnels HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Host: 172.19.2.200:8081
User-Agent: HTTPie/0.9.3

HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Date: Fri, 27 May 2016 04:13:59 GMT
Server: tman/0.1
Transfer-Encoding: chunked
```

```json
[
    {
        "dns1": "202.102.224.68",      //Server advised DNS Server
        "dns2": "202.102.227.68",
        "external": "42.235.188.158",  //Tunnel public ip
        "id": "pptp2",                 //Name
        "local": "172.17.0.2",         //Instance IP
        "port": 32772,                 //Mapped proxy port
        "server": "112.83.69.201",     //PPTP Server address
        "status": "CONNECTED",         //CONNECTED|DISCONNECTED|INITIAL
        "tunnel_ip": "172.16.254.7",   //Tunnel local address
        "user": "a051602"              //Username
    },
    {
        "dns1": "202.103.24.68",
        "dns2": "202.103.44.150",
        "external": "27.24.32.108",
        "id": "pptp1",
        "local": "172.17.0.3",
        "port": -1,
        "server": "222.186.31.224",
        "status": "DISCONNECTED",
        "tunnel_ip": "12.12.12.11",
        "user": "a051601"
    }
]
```

### `GET /tunnel/[:name]`

Get tunnel detail


```
GET /tunnel/pptp1 HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Host: 172.19.2.200:8081
User-Agent: HTTPie/0.9.3

HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Date: Fri, 27 May 2016 04:18:13 GMT
Server: tman/0.1
Transfer-Encoding: chunked
```

```json
{
    "dns1": "202.103.24.68",
    "dns2": "202.103.44.150",
    "external": "27.24.32.108",
    "id": "pptp1",
    "local": "172.17.0.3",
    "port": -1,
    "server": "222.186.31.224",
    "status": "DISCONNECTED",
    "tunnel_ip": "12.12.12.11",
    "user": "a051601"
}
```

### `POST /tunnel`

Create tunnel

#### Arguments

 - name Name of tunnel
 - server PPTP Server Address
 - user Username
 - pass Password


```
POST /tunnel HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 54
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Host: proxy-zw29-01:8081
User-Agent: HTTPie/0.9.3

name=pptp2&server=112.83.69.201&user=a051602&pass=****

HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Date: Fri, 27 May 2016 04:23:59 GMT
Server: tman/0.1
Transfer-Encoding: chunked
```

```json
{
    "dns1": "202.102.224.68",
    "dns2": "202.102.227.68",
    "external": "42.235.188.158",
    "id": "pptp2",
    "local": "172.17.0.2",
    "port": 32773,
    "server": "112.83.69.201",
    "status": "CONNECTED",
    "tunnel_ip": "172.16.254.7",
    "user": "a051602"
}
```

### `DELETE /tunnel/[:name]`

Delete Tunnel

```
DELETE /tunnel/pptp2 HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 0
Host: proxy-zw29-01:8081
User-Agent: HTTPie/0.9.3

HTTP/1.1 200 OK
Content-Type: text/plain; charset=utf-8
Date: Fri, 27 May 2016 04:25:13 GMT
Server: tman/0.1
Transfer-Encoding: chunked

pptp2
```

#`POST /tunnel/[:name]/redial`

Redial (disconnect then connect)

```
POST /tunnel/pptp1/redial HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 0
Host: proxy-zw29-01:8081
User-Agent: HTTPie/0.9.3

HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Date: Fri, 27 May 2016 04:27:18 GMT
Server: tman/0.1
Transfer-Encoding: chunked
```

```json
{
    "dns1": "202.101.224.69",
    "dns2": "202.101.226.69",
    "external": "",
    "id": "pptp1",
    "local": "172.17.0.2",
    "port": 32774,
    "server": "222.186.31.224",
    "status": "CONNECTED",
    "tunnel_ip": "12.12.12.33",
    "user": "a051601"
}
```

### `POST /tunnel/[:name]/down`

Stop instance

```
POST /tunnel/pptp1/down HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 0
Host: proxy-zw29-01:8081
User-Agent: HTTPie/0.9.3

HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Date: Fri, 27 May 2016 04:28:22 GMT
Server: tman/0.1
Transfer-Encoding: chunked
```

```json
{
    "dns1": "119.6.6.6",
    "dns2": "114.114.114.114",
    "external": "119.7.82.34",
    "id": "pptp1",
    "local": "172.17.0.2",
    "port": -1,
    "server": "222.186.31.224",
    "status": "DISCONNECTED",
    "tunnel_ip": "12.12.12.34",
    "user": "a051601"
}
```

### `POST /tunnel/[:name]/up`

Start instance

```
POST /tunnel/pptp1/up HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 0
Host: proxy-zw29-01:8081
User-Agent: HTTPie/0.9.3

HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Date: Fri, 27 May 2016 04:29:21 GMT
Server: tman/0.1
Transfer-Encoding: chunked
```

```json
{
    "dns1": null,
    "dns2": null,
    "external": null,
    "id": "pptp1",
    "local": "172.17.0.2",
    "port": 32775,
    "server": "222.186.31.224",
    "status": "INITIAL",
    "tunnel_ip": null,
    "user": "a051601"
}
```
