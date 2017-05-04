# Let’s Encrypt certificate

## For IIS

### Create new certificate

```bash
certbot certonly --manual -d www.yourwebsite.com -d yourwebsite.com
```

### Challenge

1. Create folder `[webapp root]/.well-known/acme-challenge/`. There will be placed the files that necessary to complete challenge.

2. Add a `web.config` file in previously created folder with content:
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <staticContent>
      <clear/>
      <mimeMap fileExtension = ".*" mimeType="text/plain" />
    </staticContent>
    <handlers>
      <clear />
      <add  name="StaticFile" path="*" verb="*" 
            type="" modules="StaticFileModule" scriptProcessor="" 
            resourceType="Either" requireAccess="Read" allowPathInfo="false" 
            preCondition="" responseBufferLimit="4194304" />
    </handlers>
  </system.webServer>
</configuration>
```

3. Add requested files in `[webapp root]/.well-known/acme-challenge/` and complete challenge
> Note. Check that the created file encoded in UTF-8 codepage, not in UTF-8 BOM or what else.

### Pack certificate to pkcs12 container

```bash
cd /etc/letsencrypt/live/www.yourwebsite.com/
openssl pkcs12 -in cert.pem -inkey privkey.pem -certfile chain.pem -export -name yourwebsite_date -out yourwebsite.pfx
```
