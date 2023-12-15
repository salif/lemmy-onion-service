# Lemmy Onion Service

### What is Lemmy?

Lemmy is a self-hosted social link aggregation and discussion platform.

I made this git repo for personal use for testing purposes.

## New Lemmy instance

Follow these instructions to start a new Lemmy instance using Linux and Docker.

Note that federation is not supported and there's no email server.

Clone the repo

```bash
git clone https://github.com/salif/lemmy-onion-service.git
cd ./lemmy-onion-service/
```

Use [mkp224o](https://community.torproject.org/onion-services/advanced/vanity-addresses/) to generate vanity address. Then run:

```bash
# mkp224o
mkdir -p ./volumes/lemmytor/
```

change 'example.onion' to generated address

```bash
cp example.onion/* ./volumes/lemmytor/
```

```bash
sudo chown -R 100:100 ./volumes/lemmytor
sudo chmod -R u+rwX,og-rwx ./volumes/lemmytor
mkdir volumes/pictrs
sudo chown -R 991:991 ./volumes/pictrs
```

and

```bash
cp ./templates/.env .env
```

Edit `.env` file \(domain is in `volumes/lemmytor/hostname`\) and run:

```bash
cp ./templates/nginx_internal.conf nginx_internal.conf
cp ./templates/lemmy.hjson lemmy.hjson
source .env
sed -i -e "s/_SED_1/$domain/g" lemmy.hjson
sed -i -e "s/_SED_2/$postgres_password/g" lemmy.hjson
sed -i -e "s/_SED_1/$domain/g" nginx_internal.conf
```

Start it:

```bash
sudo docker-compose up -d
```

## See also

- [join-lemmy.org/docs/administration/install_docker.html](https://join-lemmy.org/docs/administration/install_docker.html)
- [join-lemmy.org/docs/administration/tor_hidden_service.html](https://join-lemmy.org/docs/administration/tor_hidden_service.html)
