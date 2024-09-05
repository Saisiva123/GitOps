### Steps To deploy React Application to AWS S3

1. Create an IAM user with S3 Policy.
2. Setup a workflow using Github Actions.
3. Create a CI/CD pipeline by following these steps: Build, Test and Release.


### Things to acheive:
1. Make sure proper testing is done either unit tests or integration tests.
2. Make sure the PR is closed. +> Once the PR gets merged it closes automatically.
3. Make sure the branch from which the PR has been created is deleted after successfull PR merge or deployment.

### Learnings:
1. Each job runs on its own isolated environment (virtual server)
2. Sometimes of we want to share an artifact from build job to a deploy job then we could use actions
specifically to this purpose actions/upload-artifact@v3 in the build job and actions/download-artifact@v3 in the deploy job. 
3. Everytime we may checkout the code even though we have the artifact is only because sometimes we may require some deployment scripts/files that we have stored inside the repository.
4. Using default actions inside jobs makes GitOps process easier.
5. We can also have a strategy with matrix inside a job which allows us to run the job in multiple enviuronments, it creates multiple/n number of jobs that executes paralelly to ensure that the build/jobs can perfectly run in multiple environments.
6. Any files/folders that has been created in the build job (build folder that gets created once we run this job) cant be persisted in the next job as it is isolated, thats the reason we checkout in every job and use artifact upload and download options. Ofcourse in the next jobs we can keep conditions like needs the previous job to complete successfully.
7. Thats why to make it easy we can have a single job for BUILDING, TESTING and DEPLOYING as well. In that way we can have access to the build artifacts and also no need to checkout everytime.