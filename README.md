# nubis-jq

This is a small docker container (5.11MB) containing jq.

Run it like:

```bash
echo "{\"key\":\"value\"}" | docker run -i nubis-jq jq .

or

echo "{\"key\":\"value\"}" | docker run -i nubis-jq jq --raw-output .key
```

Or in a script like:

```bash
NUBIS_DEPLOY_VERSION=$(curl -k -s -S \
    "https://registry.hub.docker.com/v1/repositories/nubisproject/nubis-deploy/tags"\
    | docker run -i nubis-jq jq --raw-output '.[]["name"]' \
    | sort --field-separator=. --numeric-sort --reverse \
    | grep -m 1 "^v")
DOCKER_IMAGE="nubisproject/nubis-deploy:${NUBIS_DEPLOY_VERSION}"
echo "DOCKER_IMAGE: ${DOCKER_IMAGE}"
```
