# Dev docs

## Start the container

<!-- https://github.com/Kong/kong/blob/c17190251247b8e5f16a18a6b67ba943cdfd4615/kong.conf.default#L87 -->

docker run -d --name kong-t \
  -e "KONG_DATABASE=off" \
  -e "KONG_PROXY_ACCESS_LOG=/dev/stdout" \
  -e "KONG_ADMIN_ACCESS_LOG=/dev/stdout" \
  -e "KONG_PROXY_ERROR_LOG=/dev/stderr" \
  -e "KONG_ADMIN_ERROR_LOG=/dev/stderr" \
  -e "KONG_ADMIN_LISTEN=0.0.0.0:8001, 0.0.0.0:8444 ssl" \
  -e "KONG_PLUGINS=bundled,request-transformer-improved" \
  -e 'KONG_VAULTS=bundled,infiscal' \
  -e 'KONG_VAULT_ROTATION_INTERVAL=30' \
  -e "KONG_ERROR_DEFAULT_TYPE=application/json" \
  -e 'KONG_TRACING_INSTRUMENTATIONS=all' \
  -e 'KONG_TRACING_SAMPLING_RATE=1' \
  -e 'SECRET_VAULT_VALUE=banana1' \
  -p 8000:8000 \
  -p 8443:8443 \
  -p 8001:8001 \
  -p 8444:8444 \
  --add-host=host.docker.internal:host-gateway \
  -v /path/to/repo/kong-plugin-request-transformer-improved/plugin:/usr/local/share/lua/5.1/kong/plugins/request-transformer-improved \
  -v /path/to/repo/kong-vault-infiscal/infiscal:/usr/local/share/lua/5.1/kong/vaults/infiscal \
  -v /path/to/repo/kong-vault-infiscal/vault.lua:/opt/bitnami/kong/openresty/share/lua/5.1/kong/pdk/vault.lua \
  bitnami/kong
