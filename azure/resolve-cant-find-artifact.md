## How to resolve can't find artifacts during pipeline deployment
While trying to run a pipeline where I had put in a deployment job, the pipeline threw an error saying "Could not find any pipeline artifacts in the build". I checked the "Build" job and it said that an artifact had in fact been created. I found an [article on StackOverflow](https://stackoverflow.com/questions/56480932/use-new-deployment-job-in-azure-devops-cant-find-artifacts) that gave several explanations for issue. I ended up adding `- download: none` to fix the problem:

```
 - stage: deploy_dev
    displayName: Development environment
    jobs:
    - deployment: Deploy
      displayName: Deploy to Development environment
      environment: Production
      strategy:
        runOnce:
          deploy:
            steps:
            - download: none
            - task: DownloadBuildArtifacts@0
              inputs:
                artifactName: $(ArtifactName)
                buildType: 'current'
                downloadType: 'single'
                downloadPath: '$(System.ArtifactsDirectory)'
```
