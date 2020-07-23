# Docker DDNS Cloudflare

Simple container for setting setting and updating to your local ip address.
Only makes requests if the IP has changed since last time.
By default it runs once every minute and the IP is resolved by https://canihazip.com.

## Quickstart 🚀

1. Get yout api token [here](https://dash.cloudflare.com/) (Top right -> My Profile -> Scroll Down -> Global Api Key)

2. Create the wanted DNS record (e.g. `some.example.com`). The script can only update it, not create it.

3. Create an `.env` file:

```bash
EMAIL=my@mail.com
KEY=my_api_key
ZONE=example.org
DNS_RECORD=some.example.org
```

4. Run the container

```bash
docker run -d --name ddns --restart always --env-file .env cupcakearmy/ddns-cloudflare
```

To check logs:

```bash
docker logs ddns
```

### Docker-Copmose

With docker-compose:

```bash
git clone https://github.com/CupCakeArmy/docker-ddns-cloudflare.git
cp .sample.env .env
# Edit the .env file with your data
docker-compose up -d
```

## Customize

### Custom CRON

By default the script runs every 5 minutes. You can customize this by simply setting the `CRON` value in the `.env` file.

```bash
# .env

# e.g. every minute
CRON=* * * * *
```

### Custom Resolver

By default the script checks the own ip by calling `https://api.ipify.org/`. This also can be configured. It has to be an endpoint that return a plain text containing the ip by get request.

```bash
# .env

RESOLVER=https://ipv4.icanhazip.com/
```
