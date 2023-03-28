# docker-fortivpn-proxy ![](https://https://github.com/chussum/docker-fortivpn-proxy/workflows/Build/badge.svg)

Connect to a Fortinet SSL-VPN via http/socks5 proxy.

## Usage

NOTE: I only tested this image on macOS systems.

1. Create an openfortivpn configuration file.

    ```
    $ cat /path/to/config
    host = vpn.example.com
    port = 443
    username = foo
    password = bar
    trusted-cert = (optional)
    ```

2. Run the following command to start the container.

    ```
    $ docker container run \
        --cap-add=NET_ADMIN \
        --privileged \
        --rm \
        -v /path/to/config:/etc/openfortivpn/config:ro \
        ghcr.io/chussum/fortivpn-proxy:main
    ```

3. Now you can use SSL-VPN via `http://<container-ip>:8443` or `socks5://<container-ip>:8443`.

    ```
    $ http_proxy=http://172.17.0.2:8443 curl http://example.com

    $ ssh -o ProxyCommand="nc -x 172.17.0.2:8443 %h %p" foo@example.com
    ```

## License
MIT

thx. https://github.com/Tosainu/docker-fortivpn-socks5
