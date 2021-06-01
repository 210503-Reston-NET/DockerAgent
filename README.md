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

# Code Coverage
1. Add Packages to Your Test Project
  - https://www.nuget.org/packages/coverlet.msbuild/
  - https://www.nuget.org/packages/coverlet.collector/
  - Maybe this one too? https://www.nuget.org/packages/Microsoft.CodeCoverage/

2. Add Some stuff to your .yaml file
3. These are the Important parts:
  - SonarCloudPrepare - extraProperties
  - DotNetCoreCLI - arguements
  - PublishCoverageResults - summaryFileLocation && reportDirectory

```
- task: SonarCloudPrepare@1
    inputs:
      <Other Inputs>
      extraProperties: 'sonar.cs.opencover.reportsPaths=$(Build.SourcesDirectory)/**/coverage.opencover.xml'  
#V2
  - task: DotNetCoreCLI@2
    displayName: 'Run unit tests - $(buildConfiguration)'
    inputs:
      command: 'test'
      arguments: '--configuration $(buildConfiguration) /p:CollectCoverage=true "/p:CoverletOutputFormat=\"opencover,Cobertura\""'
      publishTestResults: true
      projects: '$(solution)'

  - task: PublishCodeCoverageResults@1
    displayName: 'Publish Code Coverage Report'
    inputs:
      codeCoverageTool: Cobertura
      summaryFileLocation: '$(Build.SourcesDirectory)/**/coverage.cobertura.xml'
      reportDirectory: '$(Build.SourcesDirectory)/App/Tests/'

```
