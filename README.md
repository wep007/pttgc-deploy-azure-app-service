# Source code scanning


## Exercise 1
### Deploy to Dev Slot
1. Login to Azure Portal, goto `App Services` then select the App service from the list
2. Go to `Overview` menu and click `Get publish profile` to download the publish profile
![Download Publish profile](./assets/get-publish-profile-01.PNG)


3. Create Secret name `AZURE_WEBAPP_PUBLISH_PROFILE` with the content from file that download
from step 2
4. Add another jobs to deploy to dev slot
```yaml
deploy-dev:
    name: Deploy to Dev Slot
    runs-on: ubuntu-latest
    needs: containerized

    steps:
      - name: deploy dev slot
        uses: azure/webapps-deploy@v2
        with:
          app-name: 'simple-service'
          # Add publish profile from secret that created from publish profile which we downloaded from Azure Portal
          publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
          images: 'repo-name/simple-service:${{ github.sha }}'
```
5. Commit and push the code, and see how the workflow is running
6. Login to Azure portal, App Service and see the changes


## Exercise 2
### Deploy to production slot


