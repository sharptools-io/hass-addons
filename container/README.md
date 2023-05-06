Container images for the SharpTools Home Assistant connection are available within our Github container repository:

https://github.com/orgs/sharptools-io/packages

You can find images for the various different architectures that Home Assistant supports.

When using the image, you will need to expose port `8099`, map the `/data` directory within the container to a directory on your host, and 
set the environment variables `STIO_HASS_URL`, `STIO_HASS_PORT`, and `STIO_HASS_TOKEN`. A description of the environment 
variables follows:


|ENV | Example | Description | 
|---|---|---|
| `STIO_HASS_URL`| `http://homeassistant.local`<br/>`http://192.168.1.10`| The base URL to your Home Assistant instance<br />(includes the protocol, but excludes the port) |
| `STIO_HASS_PORT` | `8123` | The port that your Home Assistant interface runs on |
| `STIO_HASS_TOKEN` | n/a | A [long lived access token](https://developers.home-assistant.io/docs/auth_api/#long-lived-access-token) generated from your Home Assistant profile page | 

How you run the container depends on what container orchestration platform you are using. Refer to the documentation for your container orchestratino utility for details on 
how to expose ports, map directories, or set environment variables. 

An example `docker-compose.yml` file follows:
```
version: '1'
services:
  sharptools:
    image: ghcr.io/sharptools-io/sharptools-hass-addon-connector-amd64:latest
    ports:
      - "80:8099"
    volumes:
      - /your/local/data/path:/data
    environment:
      - STIO_HASS_URL=http://homeassistant.local
      - STIO_HASS_PORT=8123
      - STIO_HASS_TOKEN=YOUR-HASS_TOKEN
```
