# docker-fortivpn-proxy ![](https://https://github.com/chussum/docker-fortivpn-proxy/workflows/Build/badge.svg)

Connect to a Fortinet SSL-VPN via socks5 proxy.

## Usage

NOTE: I only tested this image on macOS systems.

1. Create an openfortivpn configuration file.

    ```
    $ cat /path/to/config
    OPENCONNECT_URL=[server ip]:[port]
    OPENCONNECT_USER=foo
    OPENCONNECT_PASSWORD=bar
    OPENCONNECT_OPTIONS=--protocol=fortinet --servercert pin-sha256:~~~
    ```

2. Run the following command to start the container.

    ```
    $ docker run \
        -it \
        -p 1080:1080 \
        --env-file=/path/to/config \
        ghcr.io/chussum/fortivpn-proxy:main
    ```

3. Now you can use SSL-VPN via `socks5://localhost:1080`.

## License
MIT

thx. https://github.com/rankun203/openconnect-proxy
