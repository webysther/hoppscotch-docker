# hoppscotch docker

Hoppscotch image is based on PRs: [#3107](https://github.com/hoppscotch/hoppscotch/pull/3107)/[#3112](https://github.com/hoppscotch/hoppscotch/pull/3112).

Based on LSIO Images featuring:

* easy user mappings (PGID, PUID)
* custom base image with s6 overlay
* weekly base OS updates with common layers across the entire LinuxServer.io ecosystem to minimise space usage, down time and bandwidth
* regular security updates

The architecture supported by this image is:

| Architecture | Available | Tag |
| :----: | :----: | ---- |
| x86-64 | ✅ | amd64-\<version tag\> |

## Version Tags

This image provides various versions that are available via tags. Please read the descriptions carefully and exercise caution when using unstable or development tags.

| Tag | Available | Description |
| :----: | :----: |--- |
| latest | ✅ | Stable releases from Hoppscotch |

## Application Setup

- Once running the URL will be `http://<host-ip>:80` and `http://<host-ip>:80/admin` (admin).

The application accepts a series of environment variables to further customize itself on boot.

Provided by the PRs [#3107](https://github.com/hoppscotch/hoppscotch/pull/3107) and [#3112](https://github.com/hoppscotch/hoppscotch/pull/3112):

| Parameter | Function |
| :---: | --- |
| `-e MODE=` | Default is **single** but can use **nouser** or **team**|
| `-e ENABLE_ADMIN=` | Default is false. Set to true to build and run admin|
| `-e ENABLE_API=` | Default is true. Build and run backend|
| `-e ENABLE_SMTP=` | Default is true. SMTP server that redirect all e-mail to stdout|
| `-e DOMAIN=` | Default is **locahost**. |
| `-e SCHEMA=` | Default is **http**. Disable httpOnly and secure from Cookie to enable working with http. We **recommend change this when https** when available.|
| `-e PROXY_HOST=` | Default is https://proxy.hoppscotch.io. Allow change proxy host on boot|
| `-e PROXY_ENABLED=` | Default is false. Allow change proxy enabled on boot|
| `-e EXTENSIONS_ENABLED=` | Default is false. Allow change extensions on boot |
| `-e TELEMETRY_ENABLED=` | Default is true. Allow change telemetry on boot|
| `-e THEME_COLOR=` | Default is indigo, values: green, teal, blue, indigo, purple, yellow, orange, red, pink. [Allow change theme](https://docs.hoppscotch.io/documentation/features/customization) on boot|
| `-e BG_COLOR=` | Default is system, values: system, light, dark, black. [Allow background color](https://docs.hoppscotch.io/documentation/features/customization) on boot|
| `-e FONT_SIZE=` | Default is small, values: small, medium, large. [Allow change font size](https://docs.hoppscotch.io/documentation/features/customization) on boot|
| `-e ZEN_MODE=` | Default is false, [Allow change zen mode](https://docs.hoppscotch.io/documentation/features/customization) on boot|
| `-e VITE_ADMIN_BASE_URL=` | Default is /admin. Allow start admin in a custom location|
| `-e SMTP_PROTOCOL=` | Default is smtp, values: smtp or smtps|
| `-e SMTP_DOMAIN=` | Default is localhost|
| `-e SMTP_PORT=` | Default is 25|
| `-e SMTP_USER=` | Default is nouser|
| `-e SMTP_PASSWORD=` | Default is nopass|
| `-e POSTGRES_HOST=` | Default is hoppscotch-db|
| `-e POSTGRES_PORT=` | Default is 5432|
| `-e POSTGRES_DB=` | Default is hoppscotch|
| `-e POSTGRES_USER=` | Default is postgres|
| `-e POSTGRES_PASSWORD=` | postgres password|

Provided by [hoppscotch](https://docs.hoppscotch.io/documentation/self-host/install-and-build/#configuring-the-environment):

| Parameter | Function |
| :---: | --- |
| `-e DATABASE_URL=` | Default is postgresql://postgres:testpass@hoppscotch-db:5432/hoppscotch if set the individual values for database are ignored.|
| `-e JWT_SECRET=` | Created on boot if not set. If not set by user not persist when container is recreated. |
| `-e SESSION_SECRET=` | Created on boot if not set. If not set by user not persist when container is recreated. |
| `-e PRODUCTION=` | Default is true. |
| `-e TOKEN_SALT_COMPLEXITY=` | Default is 10. |
| `-e MAGIC_LINK_TOKEN_VALIDITY=` | Default is 3. |
| `-e REFRESH_TOKEN_VALIDITY=` | Default is 604800000 (7 days). |
| `-e ACCESS_TOKEN_VALIDITY=` | Default is 86400000 (1 day). |
| `-e REDIRECT_URL=` | Default is SCHEMA+DOMAIN. |
| `-e WHITELISTED_ORIGINS=` | Default is SCHEMA+DOMAIN. |
| `-e VITE_BASE_URL=` | Default is SCHEMA+DOMAIN. |
| `-e VITE_SHORTCODE_BASE_URL=` | Default is SCHEMA+DOMAIN. |
| `-e VITE_BACKEND_API_URL=` | Default is SCHEMA+DOMAIN/api/v1. |
| `-e VITE_BACKEND_GQL_URL=` | Default is SCHEMA+DOMAIN/api/graphql. |
| `-e VITE_BACKEND_WS_URL=` | Default is wss://DOMAIN/api/graphql. |
| `-e VITE_ADMIN_URL=` | Default is SCHEMA+DOMAIN+VITE_ADMIN_BASE_URL. |
| `-e VITE_APP_TOS_LINK=` | Default is https://docs.hoppscotch.io/support/terms. |
| `-e VITE_APP_PRIVACY_POLICY_LINK=` | Default is https://docs.hoppscotch.io/support/privacy. |
| `-e GOOGLE_CLIENT_ID=` | Default is empty. |
| `-e GOOGLE_CLIENT_SECRET=` | Default is empty. |
| `-e GOOGLE_CALLBACK_URL=` | Default is SCHEMA+DOMAIN/v1/auth/google/callback. |
| `-e GOOGLE_SCOPE=` | Default is **email,profile**. |
| `-e GITHUB_CLIENT_ID=` | Default is empty. |
| `-e GITHUB_CLIENT_SECRET=` | Default is empty. |
| `-e GITHUB_CALLBACK_URL=` | Default is SCHEMA+DOMAIN/v1/auth/github/callback. |
| `-e GITHUB_SCOPE=` | Default is **user:email**. |
| `-e MICROSOFT_CLIENT_ID=` | Default is empty. |
| `-e MICROSOFT_CLIENT_SECRET=` | Default is empty. |
| `-e MICROSOFT_CALLBACK_URL=` | Default is SCHEMA+DOMAIN/v1/auth/microsoft/callback. |
| `-e MICROSOFT_SCOPE=` | Default is **user.read**. |
| `-e MAILER_ADDRESS_FROM=` | Default is 'SMTP_USER <SMTP_USER@SMTP_DOMAIN>'. if set the individual values for mailer are ignored. |
| `-e MAILER_SMTP_URL=` | Default is 'SMTP_PROTOCOL://SMTP_USER@DOMAIN:SMTP_PASSWORD@SMTP_DOMAIN:SMTP_PORT. if set the individual values for smtp are ignored. |

## Usage

Here are some example snippets to help you get started creating a container.

### docker-compose (recommended, [click here for more info](https://docs.linuxserver.io/general/docker-compose))

```yaml
---
version: "2.1"
services:
  hoppscotch:
    image: webysther/hoppscotch:latest
    container_name: hoppscotch
    ports:
      - 80:80
    restart: unless-stopped
```

### docker cli ([click here for more info](https://docs.docker.com/engine/reference/commandline/cli/))

```bash
docker run -d \
  --name=hoppscotch \
  -p 80:80 \
  --restart unless-stopped \
  webysther/hoppscotch:latest
```

### docker-compose with database

```yaml
---
version: "2.1"
services:
  hoppscotch:
    image: webysther/hoppscotch:latest
    container_name: hoppscotch
    networks:
      hoppscotch:
      hoppscotch-db:
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - POSTGRES_PASSWORD=password-for-database
    volumes:
      - /path/to/hoppscotch/config:/config
    ports:
      - 80:80
    depends_on:
      hoppscotch-db:
        condition: service_healthy
    restart: unless-stopped

  hoppscotch-db:
    image: postgres:alpine
    container_name: hoppscotch-db
    networks:
      hoppscotch-db:
    environment:
      - POSTGRES_DB=hoppscotch
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=password-for-database
    volumes:
      - /path/to/postgres/data:/var/lib/postgresql/data
    expose:
      - 5432
    healthcheck:
      test: [
        "CMD-SHELL", 
        "sh -c 'pg_isready -U ${POSTGRES_USER} -d ${POSTGRES_DB}'"
      ]
      interval: 10s
      timeout: 5s
      retries: 5
    restart: unless-stopped

networks:
  hoppscotch:
    name: hoppscotch
  hoppscotch-db:
    name: hoppscotch-db
```

### docker-compose for teams

```yaml
---
version: "2.1"
services:
  hoppscotch:
    image: webysther/hoppscotch:latest
    environment:
      - MODE=team
      - DATABASE_URL=postgresql://postgres:testpass@hoppscotch-db:5432/hoppscotch
    volumes:
      - /path/to/hoppscotch/config:/config
    ports:
      - 80:80
    restart: unless-stopped
```

### docker-compose with UX customization

```yaml
---
version: "2.1"
services:
  hoppscotch:
    image: webysther/hoppscotch:latest
    environment:
      - THEME_COLOR=orange
      - BG_COLOR=dark
      - FONT_SIZE=large
      - ZEN_MODE=true
      - EXTENSIONS_ENABLED=true
      - TELEMETRY_ENABLED=false
      - DATABASE_URL=postgresql://postgres:testpass@hoppscotch-db:5432/hoppscotch
    volumes:
      - /path/to/hoppscotch/config:/config
    ports:
      - 80:80
    restart: unless-stopped
```

### docker-compose multiple container

This configuration can be expanded to every service in container.

```yaml
---
version: "2.1"
services:
  hoppscotch:
    image: webysther/hoppscotch:latest
    container_name: hoppscotch
    networks:
      hoppscotch:
    environment:
      - VITE_BACKEND_API_URL=http://hoppscotch-api/api/v1
      - VITE_BACKEND_GQL_URL=http://hoppscotch-api/api/graphql
      - VITE_BACKEND_WS_URL=wss://hoppscotch-api/api/graphql
    ports:
      - 80:80
    restart: unless-stopped

  hoppscotch-api:
    image: webysther/hoppscotch:latest
    container_name: hoppscotch
    networks:
      hoppscotch:
      hoppscotch-db:
    environment:
      - POSTGRES_PASSWORD=password-for-database
    ports:
      - 8080:3170
    restart: unless-stopped

  hoppscotch-db:
    image: postgres:alpine
    container_name: hoppscotch-db
    networks:
      hoppscotch-db:
    environment:
      - POSTGRES_DB=hoppscotch
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=password-for-database
    volumes:
      - /path/to/postgres/data:/var/lib/postgresql/data
    expose:
      - 5432
    restart: unless-stopped

networks:
  hoppscotch:
    name: hoppscotch
  hoppscotch-db:
    name: hoppscotch-db
```

### Feature: MODE

MODE is ENV variable with default value of **single** and is used to start all services but admin.

The mode nouser is focused in use standalone without need to have a user, this mode disable SMTP Server and enable ZEN_MODE by default.

The mode team enable admin.

```yaml
---
...
    environment:
      - MODE=single|nouser|team
...
```

## Feature: Login with SMTP

By default a SMTP server spinup to provide the login facilite by e-mail direct in your docker log.
After put you e-mail the click to send a link you be logged to the docker logs, please use this link to login.
We recommend to setup a safe SMTP or OAUTH.

## Feature: HTTP

By default the current distribution of hoppscotch don't allow you login using http, this is fixed in this PR and can be changed by the ENV SCHEMA.

```
*****************************************************
INFORMATION
Keep in mind to work in SCHEMA HTTP is necessary
disable 2 security features: httpOnly and secure
- If you is using a reverse proxy you good to go
- Don't use this option direct exposed in production!
*****************************************************
```

## Feature: Build skipped

The current hoppscotch need to be build every time if you change any ENV values, in this PR this the build process is skipped if the ENV don't change, this will **not** happen if you don't set JWT_SECRET and SESSION_SECRET, because the key is recreated every time the container is restarted.

```
************************************************
WARNING
JWT_SECRET is automatic created but not
persist when container is recreated, set to fix.
************************************************

************************************************
WARNING
SESSION_SECRET is automatic created but not
persist when container is recreated, set to fix.
************************************************
```

## Parameters

Container images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

| Parameter | Function |
| :----: | --- |
| `-p 80` | Allows HTTP access to the internal webserver. |
| `-e PUID=1000` | for UserID - see below for explanation |
| `-e PGID=1000` | for GroupID - see below for explanation |
| `-e TZ=Etc/UTC` | specify a timezone to use, see this [list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List). |
| `-v /config` | Hoppscotch data |

## Environment variables from files (Docker secrets)

You can set any environment variable from a file by using a special prepend `FILE__`.

As an example:

```bash
-e FILE__PASSWORD=/run/secrets/mysecretpassword
```

Will set the environment variable `PASSWORD` based on the contents of the `/run/secrets/mysecretpassword` file.

## User / Group Identifiers

When using volumes (`-v` flags) permissions issues can arise between the host OS and the container, we avoid this issue by allowing you to specify the user `PUID` and group `PGID`.

Ensure any volume directories on the host are owned by the same user you specify and any permissions issues will vanish like magic.

In this instance `PUID=1000` and `PGID=1000`, to find yours use `id user` as below:

```bash
  $ id username
    uid=1000(dockeruser) gid=1000(dockergroup) groups=1000(dockergroup)
```

## Docker Mods

[![Docker Universal Mods](https://img.shields.io/badge/dynamic/yaml?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=universal&query=%24.mods%5B%27universal%27%5D.mod_count&url=https%3A%2F%2Fraw.githubusercontent.com%2Flinuxserver%2Fdocker-mods%2Fmaster%2Fmod-list.yml)](https://mods.linuxserver.io/?mod=universal "view available universal mods.")

LinuxServer publish various [Docker Mods](https://github.com/linuxserver/docker-mods) to enable additional functionality within the containers. The list of Mods available for this image (if any) as well as universal mods that can be applied to any one of our images can be accessed via the dynamic badges above.

## Support Info

* Shell access whilst the container is running: `docker exec -it hoppscotch /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f hoppscotch`
* container version number
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' hoppscotch`

## Updating Info

This image is static, versioned, and require an image update and container recreation to update the app inside.
Below are the instructions for updating containers:

### Via Docker Compose

* Update all images: `docker-compose pull`
  * or update a single image: `docker-compose pull hoppscotch`
* Let compose update all containers as necessary: `docker-compose up -d`
  * or update a single container: `docker-compose up -d hoppscotch`
* You can also remove the old dangling images: `docker image prune`

### Via Docker Run

* Update the image: `docker pull webysther/hoppscotch:latest`
* Stop the running container: `docker stop hoppscotch`
* Delete the container: `docker rm hoppscotch`
* Recreate a new container with the same docker run parameters as instructed above (if mapped correctly to a host folder, your `/config` folder and settings will be preserved)
* You can also remove the old dangling images: `docker image prune`

### Via Watchtower auto-updater (only use if you don't remember the original parameters)

* Pull the latest image at its tag and replace it with the same env variables in one run:

  ```bash
  docker run --rm \
  -v /var/run/docker.sock:/var/run/docker.sock \
  containrrr/watchtower \
  --run-once bazarr
  ```

* You can also remove the old dangling images: `docker image prune`

**Note:** We do not endorse the use of Watchtower as a solution to automated updates of existing Docker containers. In fact we generally discourage automated updates. However, this is a useful tool for one-time manual updates of containers where you have forgotten the original parameters. In the long term, we highly recommend using [Docker Compose](https://docs.linuxserver.io/general/docker-compose).

## Building locally

If you want to make local modifications to these images for development purposes or just to customize the logic:

```bash
git clone https://github.com/webysther/hoppscotch-docker.git
cd hoppscotch-docker
docker build --build-arg HOPPSCOTH_RELEASE="2023.4.7" . -t webysther/hoppscotch:2023.4.7 -t webysther/hoppscotch:latest
docker push webysther/hoppscotch --all-tags
```
