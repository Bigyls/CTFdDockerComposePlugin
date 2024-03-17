# CTFd Docker Compose Plugin

![CTFd version](https://shields.io/badge/WorkOn-CTFd>=3.6.0-green?&style=for-the-badge)

This CTFd plugin allows you to run ephemeral multi-container applications using [Docker Compose](https://docs.docker.com/compose/) for specific challenges. Users and Teams can request a container to use as needed, and its lifecycle will be managed by the plugin.

It's possible to run [CTFd Docker Containers Plugin](https://github.com/Bigyls/CTFdDockerContainersPlugin) at the same time.

> [!NOTE]  
>This is different than launching CTFd with Docker Compose

## Usage

### Installation

Go to your CTFd/plugins folder and execute following commands:

```shell
git clone https://github.com/Bigyls/CTFdDockerComposePlugin.git composes
```

### Configuration

To configure the plugin, go to the admin page, click the dropdown in the navbar for plugins, and go to the Composes page (https://example.com/composes/settings).

Then you can click the settings button to configure the connection. You will need to specify the connection method to use. This can either be the local Unix socket or an TCP connection. If using Docker Compose CTFd installation, you can map docker socket into CTFd container by modifying the docker-compose.yml file:

```yml
 services:
   ctfd:
     ...
     volumes:
     ...
       - /var/run/docker.sock:/var/run/docker.sock
     ...
```

After saving, the plugin will try to connect to the Docker daemon and the status should show as an error message or as a green symbol (maybe restart ctf to be sure).

To create challenges, use the container challenge type and configure the options. It is set up with dynamic scoring, so if you want regular scoring, set the maximum and minimum to the same value and the decay to zero.

It's also possible to configure auto deployment using [ctfcli](https://github.com/CTFd/ctfcli) and its YAML configuration:

```yaml
name: BestChallenge
...
type: compose
value: 50
extra:
  initial: 50
  decay: 75
  minimum: 10
  image: /path/to/docker-compose.yml
  port: 1337

connection_info: https://container.example.com
...
```

When a user clicks on a Docker Compose challenge, a button labeled "Start Lab" appears. Clicking it shows the information below with a random port assignment.

## Roadmap

- [ ] Create the plugin.
- [ ] Possibility to use 2 docker TCP connection method (like 1 windows and 1 linux).
- [ ] Make it work with User mode.
- [ ] Make it work with Team mode.

## Contributing

You can create issues and PRs by yourself if you experienced a bug, have questions or if you have an idea for a new feature. This repository aims to remain active, up to date and scalable.

## Credits

Based on https://github.com/Bigyls/CTFdDockerContainersPlugin.
