# Infrastructure

## Servers

Hosting provider: [Amazon]()

| Domain               | IP             | City    | CPU | RAM   | DRIVE  | $/mo |
| -------------------- | -------------- | ------- | --- | ----- | ------ | ---- |
| dmzdev.xyz           | 44.193.217.174 | Ashburn | 4   | 16 GB | 120 GB |      |
| dev.dmzdev.xyz       |                |         | 4   | 16 GB | 120 GB |      |
| ipfs.dmzdev.xyz      | 44.193.217.174 |         | 1   |       |        |      |
| indexator.dmzdev.xyz | 44.193.217.174 |         | 1   |       |        |      |
| content.dmzdev.xyz   | 44.193.217.174 |         | 1   |       |        |      |
| app.dmzdev.xyz       | 44.193.217.174 |         | 1   |       |        |      |
| vpn.dmzdev.xyz       | 44.193.217.174 |         | 1   |       |        |      |
| monitor.dmzdev.xyz   |                |         | 1   |       |        |      |

```
old - numiz.xyz
```

## Server initialization with [ansible](https://www.ansible.com)

```shell
ansible-playbook -vvvi playbook/inventory/all.yaml playbook/init.yaml
```

## Prepare to up local

```shell
docker network create traefik
```

## Up local

```shell
docker compose --env-file .env.local up
```

- [traefik.localhost](http://traefik.localhost)
- [metrics.traefik.localhost](http://metrics.traefik.localhost)
- [whoami.localhost](http://whoami.localhost)
- [node.localhost](http://node.localhost)
- [vpn.localhost](http://vpn.localhost)
- [ipfs.localhost/webui](http://ipfs.localhost/webui)
- [content.localhost](http://content.localhost)
- [grafana.monitor.localhost](http://grafana.monitor.localhost)
- [prometheus.monitor.localhost](http://prometheus.monitor.localhost)
- [consul.monitor.localhost](http://consul.monitor.localhost)

Default basic auth: `admin`:`admin`

## Important!

**DO NOT USE LOCAL UP IN PRODUCTION**

Use GitHub actions for production deployment

## GitHub secrets

- `NMZ_GIT_ACTIONS` - SSH private key for `playbook/ssh/github.pub`
- `BASIC_AUTH_USER` - [HTTP authentication](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication) username for administrator subdomains like `traefik`
- `BASIC_AUTH_PASSWORD` - [HTTP authentication](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication) password for administrator subdomains like `traefik`
- `VPN_UI_PASSWORD` - password for [wg-easy](https://github.com/WeeJeWel/wg-easy) UI
