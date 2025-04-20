Here’s the generic curl syntax for fetching your application’s configuration from a Spring Cloud Config Server:

```bash
curl -H "Accept: application/json" \
  http://<config-server-host>:<port>/{application}/{profile}/{label}
```

- **`<config-server-host>`**: the hostname (e.g. `localhost`)
- **`<port>`**: the port your Config Server listens on (e.g. `8888`)
- **`{application}`**: the value of `spring.application.name` in your client app
- **`{profile}`**: the Spring profile(s) you want (e.g. `default`, `dev,prod`)
- **`{label}`**: the Git label/branch (e.g. `main`, `release-1.0`)

---

### Examples

1. **JSON output** (default):
   ```bash
   curl -H "Accept: application/json" \
     http://localhost:8888/catalog-service/default/main
   ```

2. **YAML output**:
   ```bash
   curl -H "Accept: application/x-yaml" \
     http://localhost:8888/catalog-service/default/main
   ```

3. **Raw properties file**:
   ```bash
   curl http://localhost:8888/catalog-service/default/main/application.properties
   ```

4. **Fetch only a specific file** (e.g. `application-dev.yml`):
   ```bash
   curl http://localhost:8888/catalog-service/dev/main/application-dev.yml
   ```

5. **Combine multiple profiles**:
   ```bash
   curl http://localhost:8888/catalog-service/dev,qa/main
   ```

---

You can also append query parameters, for example to include native overrides or skip decryption:

```bash
curl "http://localhost:8888/catalog-service/default/main?encrypt=false&nativeSearchLocations=true"
```

Use these templates to point any client—or even a simple script—at your Config Server’s REST API.