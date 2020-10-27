# Manual Agent in Linux

Agent is the application to run jobs, you have to create an Agent before job started.

> if installed from [docker-install](https://github.com/FlowCI/docker-install.git) repo, there are default dynamic Agent configuread locally, which means you can start build without agent setup.

## Create an Agent from admin page

* Click `Settings` -> `Agents` -> `+`
* Select `Manual agent`
* Specify unique agent name
* Specify tag (optional)

    Agent tag is used for flow which has `selector` configuration in YAML, that means the flow job runs only on the agent with matched tags.

    For example, if YAML specified `selector` like the following, so that job will runs only on Agents with tag `ios`.

    ```yaml
    selector:
      label:
        - ios
    ```

* Click `Save`

    The created agent will be shown on the list

![how to create agent](../../src/agents/create_agent.gif)

## Start Agent

Set flow.ci server url and token copied from admin page as arguments

> you can find lastet version from [agent release](https://github.com/FlowCI/flow-agent-x/releases)

### Docker

The most easiest way is start agent from [docker-install](https://github.com/flowci/docker-install) repo by run `./agent.sh` script.

Or start from the following script, and replace the value of `FLOWCI_SERVER_URL` and `FLOWCI_AGENT_TOKEN`

```bash
docker volume create pyenv
docker run --rm -v pyenv:/ws flowci/pyenv:1.0 bash -c "~/init-pyenv-volume.sh"

docker run -it \
-e FLOWCI_SERVER_URL=<http://yourhost:port> \
-e FLOWCI_AGENT_TOKEN=<token_copied_from_admin_page> \
-e FLOWCI_AGENT_VOLUMES="name=pyenv,dest=/ci/python,script=init.sh" \
-v /var/run/docker.sock:/var/run/docker.sock \
flowci/agent
```

### Linux

```bash
wget https://github.com/FlowCI/flow-agent-x/releases/download/v0.20.45/flow-agent-x-linux
chmod +x flow-agent-x-linux
./flow-agent-x-linux -u <ci_server_url> -t <agent_token>

# ex: ./flow-agent-x-linux -u http://172.10.20.1:8080 -t 44793491-03ac-4a3c-8c59-1f09b7c9d0e3
```

## MacOS

```bash
wget https://github.com/FlowCI/flow-agent-x/releases/download/v0.20.45/flow-agent-x-mac
chmod +x flow-agent-x-mac
./flow-agent-x-mac -u <ci_server_url> -t <agent_token>

# ex: ./flow-agent-x-linux -u http://172.10.20.1:8080 -t 44793491-03ac-4a3c-8c59-1f09b7c9d0e3
```

## Windows (x64)

```powershell
wget https://github.com/FlowCI/flow-agent-x/releases/download/v0.20.45/flow-agent-x-win
chmod +x flow-agent-x-win
./flow-agent-x-linux -u <ci_server_url> -t <agent_token>

# ex: ./flow-agent-x-linux -u http://172.10.20.1:8080 -t 44793491-03ac-4a3c-8c59-1f09b7c9d0e3
```

