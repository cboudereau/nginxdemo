# mirror

repeat the incoming requests to all backends by transferring the first response but awaiting result from all backends

In the docker compose example, the repeater service proxies the website and repeats the request to website-mirror by discarding the result. 
As a demo, the website-mirror conf is buggy (missing the /data/www directory) but the curl call response is ok since the proxied website has a valid config.

```bash
docker compose down --remove-orphans -v --rmi local && docker compose up
```

will output
```bash
mirror-website-mirror-1  | 2023/08/28 14:34:44 [error] 29#29: *1 "/data/www/index.html" is not found (2: No such file or directory), client: 192.168.112.4, server: localhost, request: "GET / HTTP/1.0", host: "mirror_backend"
mirror-website-mirror-1  | 192.168.112.4 - - [28/Aug/2023:14:34:44 +0000] "GET / HTTP/1.0" 404 153 "-" "curl/8.1.2"
mirror-website-1         | 192.168.112.4 - - [28/Aug/2023:14:34:44 +0000] "GET / HTTP/1.0" 200 11 "-" "curl/8.1.2"
mirror-repeater-1        | 192.168.112.5 - - [28/Aug/2023:14:34:44 +0000] "GET / HTTP/1.1" 200 11 "-" "curl/8.1.2"
mirror-curl-1            | < HTTP/1.1 200 OK
...
mirror-curl-1            | <
mirror-curl-1            | { [11 bytes data]
100    11  100    11    0     0   1483      0 --:--:-- --:--:-- --:--:--  1571
mirror-curl-1            | * Connection #0 to host repeater left intact
mirror-curl-1            | Hello world
mirror-curl-1 exited with code 0
```