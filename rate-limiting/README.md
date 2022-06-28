# rate-limiting

nginx using limit_req module to limit 10MB of addresses to 12 requests per minutes with a burst of 5 then replying 429 Too many requests

source : http://nginx.org/en/docs/http/ngx_http_limit_req_module.html

```bash
docker compose up
```

```bash
watch -n 2 -d -- curl http://localhost
```