---
description: >-
  Gamma is a personal Orbs blockchain running locally that allows developers to easily test, run, and deploy smart contracts.
---

# Installing Gamma - local blockchain

## Prerequisite

Gamma uses [Docker](https://www.docker.com/) to run a personal blockchain with multiple nodes locally. Make sure Docker is available on your machine. 

### On MAC
See installation instructions [here](https://docs.docker.com/docker-for-mac/install/).

### On Linux
Install the community edition using the convenience script
 [here](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-convenience-script).

## Installing Gamma Command Line Tool

Next, install the Gamma CLI. `gamma-cli` is the command line tool for developers to interact with a Gamma server instance running on their machine.

### On Mac
Use [brew](https://brew.sh/)

```
brew install orbs-network/devtools/gamma-cli
```
### On Linux
Run the gamma-cli install script in terminal:
```bash
https://raw.githubusercontent.com/orbs-network/gamma-cli/master/gammacli-linux-install-v0.7.0.sh | bash
```

### Verify
Verify the installation by running:
```text
gamma-cli version
```

## Using Gamma CLI

You can see the various commands supported by the CLI by running in terminal

```text
gamma-cli help
```

You can use the CLI to start and stop Gamma server, deploy contracts and send transactions.

## Installing the Gamma server

Gamma server is an in-memory virtual chain on top of an Orbs blockchain with several nodes on your local machine. The server allows you to test your contracts locally before deploying them to production.

If the server isn't installed yet, `gamma-cli` installs it automatically.

So far, we only installed the cli tool. Now, start the Gamma server by running the following command in the terminal. The CLI tool will notice the server is not installed and will install it for you: 

```text
gamma-cli start-local
```

If everything went well, you now have a running ORBS blockchain on your local machine. Yes, it's that simple! You can browse to http://localhost:8080/ to view the status of your local ORBS instance.

The `start-local` comands also runs our block explorer, Prism. You can use Prism to get more info about your blockchain instance by browsing to http://localhost:3000/. 

When finished with the server, stop it by running in terminal

```text
gamma-cli stop-local
```

