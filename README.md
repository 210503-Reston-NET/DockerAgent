# How to setup Docker build agent:
These are where my info came from:
- https://docs.microsoft.com/en-us/dotnet/core/install/linux-ubuntu
- https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops

## Build and run the image
1. `docker build -t dockeragent:latest .`
2. `docker run -e AZP_URL=<Azure DevOps instance> -e AZP_TOKEN=<PAT token> -e AZP_AGENT_NAME=mydockeragent dockeragent:latest`
