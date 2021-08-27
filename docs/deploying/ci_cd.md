# CI/CD 

Continuous Integration and Continuous Deployment/Delivery are fundamental DevOps best pratices where develoeprs merge changes into a central repository where automated buils and checks run and then auto-deployed. 

We run our CIs on gitlab and use ArgoCD to deploy code to our kubernetes clusters. 
A thorough explaination of our CI/CD architecture and how to use it can be found [here](https://outline.vernacular.ai/doc/build-and-deploy-using-cicd-TQrnrCpBox).

Once you've gone through the documentation, here is a short excerise to help you get some hands-on experience with the process:

1. Create a new repository on Gitlab with the name `<your-name>-starter-sample`.
2. Copy all files from [skit-starter-sample](https://gitlab.com/vernacularai/starter-sample) ( Forking a project under the same namespace in not available in Gitlab)
3. Modify the following line in `main.py` to print your message instead of `Hello!`
    ```
    cowsay.cow("Hello!")
    ```
4. Create an ECR repository with the name as `<your-name>-starter-sample` in AWS ECR.
5. Go through and modify the `.gitlab-ci.yml` file by changing APP_NAME and SERVICE_NAME variables with your service name which is `<your-name>-starter-sample`
6. Merge your changes and tag with `v0.0.1-0.0.1` to trigger docker build and deploy steps.
7. Once the image is built, confirm it's been uploaded in AWS ECR. 
8. Next, clone the [k8s-configs](https://gitlab.com/vernacularai/kubernetes/k8s-configs). Create your own branch and copy the helm chart fodler [starter-sample](link) and rename the folder to `<your-name>-starter-sample`.
9. Change all occurances of `starter-sample` to `<your-name>-starter-sample` in `Chart.yaml`, `application-staging.yaml` and `values-staging.yaml`.
10. Merge your branch.  Once the post-merge pipeline passes, search for your application in [ArgoCD](https://argocd.vernacular.ai). 
11. It should be green and healthy. Check the logs to confirm if the cow is saying the text you've provided. Get the deployment verified by your buddy. 

Once verififcation is done, complete the following cleanup activities-
1. Delete your deployment from ArgoCD using the Delete option in the UI.
2. Delete your helm chart from `k8s-configs` repository.
3. Delete the ECR repository created by you. 
4. Delete your gitlab repository. 