# How to setup Docker build agent:
These are where my info came from:
- https://docs.microsoft.com/en-us/dotnet/core/install/linux-ubuntu
- https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops

## Build and run the image
Mac + Linux
1. `docker build -t dockeragent:latest .`
2. `docker run -e AZP_URL=https://dev.azure.com/<ORGANIZATION NAME HERE> -e AZP_TOKEN=<PAT TOKEN HERE> -e AZP_AGENT_NAME=mydockeragent dockeragent:latest`

## Windows Instructions
Open Git Bash

1. `git clone https://github.com/210503-Reston-NET/DockerAgent.git`

2. `cd DockerAgent`

3. `docker build -t dockeragent:latest .`

4. `docker run -e AZP_URL=https://dev.azure.com/<ORGANIZATION NAME HERE> -e AZP_TOKEN=<PAT TOKEN HERE> -e AZP_AGENT_NAME=mydockeragent dockeragent:latest`


If you get an error: `exec user process caused: no such file or directory`

 - Run: `dos2unix start.sh`

Then Repeat steps 3 and 4 (The build will run much faster)

If you get other errors, message me :)

### Git bash converts unix style line endings to some windows garbage by default.
### The docker image needs the unix style ending because it is a linux operating system.
