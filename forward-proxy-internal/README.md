# nginx forward-proxy-internal

- Run the forward proxy on 8080 host port
```bash
docker compose down --remove-orphans -v --rmi local && docker compose up
```

- Test the forward proxy
```bash
curl http://www -x http://localhost:8080
```
