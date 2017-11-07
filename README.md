# cURL

cURL supports by Alpine in a docker container.

[![](https://img.shields.io/badge/Github-thxcode/curl-orange.svg)](https://github.com/thxcode/curl)&nbsp;[![](https://img.shields.io/badge/Docker_Hub-maiwj/curl-orange.svg)](https://hub.docker.com/r/maiwj/curl)&nbsp;[![](https://img.shields.io/docker/build/maiwj/curl.svg)](https://hub.docker.com/r/maiwj/curl)&nbsp;[![](https://img.shields.io/docker/pulls/maiwj/curl.svg)](https://store.docker.com/community/images/maiwj/curl)&nbsp;[![](https://img.shields.io/github/license/thxcode/curl.svg)](https://github.com/thxcode/curl)

[![](https://images.microbadger.com/badges/image/maiwj/curl.svg)](https://microbadger.com/images/maiwj/curl)&nbsp;[![](https://images.microbadger.com/badges/version/maiwj/curl.svg)](http://microbadger.com/images/maiwj/curl)&nbsp;[![](https://images.microbadger.com/badges/commit/maiwj/curl.svg)](http://microbadger.com/images/maiwj/curl.svg)

## References

- [cURL](https://curl.haxx.se/docs/manpage.html)
- [jq](https://stedolan.github.io/jq/)
- [Kubernetes RESTful API](https://kubernetes.io/docs/reference/)

## How to use this image

### Start an instance

To start a container, use the following:

``` bash
$ docker run -it --name test-curl maiwj/curl
```

### Watching resources from Kubernetes Pod

``` bash
$ kubectl run -it --image maiwj/curl:latest test bash

/# export CACERT_PATH=/var/run/secrets/kubernetes.io/serviceaccount/ca.crt

/# export TOKEN_CONTENT=$(cat /var/run/secrets/kubernetes.io/serviceaccount/token)

/# export NAMESPACE=$(cat /var/run/secrets/kubernetes.io/serviceaccount/namespace)

/# curl --cacert $CACERT_PATH \
--header "Authorization: Bearer $TOKEN_CONTENT" --header "Connection: Keep-Alive" \
--silent --no-buffer \
-X GET "https://kubernetes/api/v1/watch/namespaces/$NAMESPACE/pods" | jq 'if (.object.status.conditions | length) > 0 and (.object.status.conditions | map(select(.type=="Ready" and .status=="True")) | length) > 0 then {type: .type, name: .object.metadata.name} else empty end'

```

## License

- cURL is released under the [MIT License](https://curl.haxx.se/docs/copyright.html)
- This image is released under the [MIT License](LICENSE)
