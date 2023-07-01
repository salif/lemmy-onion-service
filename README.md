# Start Lemmy Onion Service

Use [mkp224o](https://community.torproject.org/onion-services/advanced/vanity-addresses/) to generate vanity address. Then run:

```
mkdir -p ./volumes/lemmytor/
```

change 'example.onion' to generated address

```
cp example.onion/* ./volumes/lemmytor/
```

```
sudo chown -R 100:100 ./volumes/lemmytor
sudo chmod -R u+rwX,og-rwx ./volumes/lemmytor
mkdir volumes/pictrs
sudo chown -R 991:991 ./volumes/pictrs
```

and

```
cp .env.template .env
```

Edit `.env` file \(domain is in `volumes/lemmytor/hostname`\) and run:

```
cp nginx_internal.conf.template nginx_internal.conf
cp lemmy.hjson.template lemmy.hjson
source .env
sed -i -e "s/SED1Z/$domain/g" lemmy.hjson
sed -i -e "s/SED2Z/$postgres_password/g" lemmy.hjson
sed -i -e "s/SED1Z/$domain/g" nginx_internal.conf
```

Start it:

```
sudo docker-compose up -d
```

## See also

- [join-lemmy.org/docs/administration/install_docker.html](https://join-lemmy.org/docs/administration/install_docker.html)
- [join-lemmy.org/docs/administration/tor_hidden_service.html](https://join-lemmy.org/docs/administration/tor_hidden_service.html)
