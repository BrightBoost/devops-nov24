### Step 1: Set up the Demo Project on GitHub
1. **Fork the Repository**: Go to the demo project [here](https://github.com/BrightBoost/deploy-azure) and fork it to your GitHub account. This will allow you to make changes and connect it to Azure DevOps for deployment.

### Step 2: Create an Azure Web App for Hosting
1. **Login to Azure Portal**: Go to [https://portal.azure.com/](https://portal.azure.com/) and log in with your Azure credentials. If prompted, create a new password and save it securely.
2. **Navigate to App Service**: In the Azure portal, search for **App Service** in the top search bar and select it.
3. **Create a New Web App**:
   - Click **Create**.
   - Choose **Web App** as the service.
   - Fill in the following details:
     - **Name**: e.g., `demonodeapp20` (this will be part of the app's URL).
     - **Runtime stack**: Choose **Node 20 LTS**.
     - **Region**: Select a region closest to you.
     - **Pricing plan**: Select **Free F1**.
   - Click **Review + Create**.
4. **Deploy the Web App**: Click **Create** to deploy the web app. Wait for the deployment to complete; you’ll see a notification when it’s ready.

### Step 3: Set up Azure DevOps
1. **Go to Azure DevOps**: Visit [Azure DevOps](https://azure.microsoft.com/en-us/products/devops/) and click on **Start Free**.
2. **Set Up DevOps Organization**:
   - Log in and create an organization if you don’t have one. Leave the default organization name and choose **United States** for project hosting.
   - Solve the CAPTCHA.
3. **Create a New Project**:
   - Once your Azure DevOps organization is ready, click **Create Project**.
   - Name it `DemoNode` and click **Create**.

### Step 4: Set Up a Pipeline for Continuous Deployment
1. **Go to Pipelines**: In your Azure DevOps project, click on **Pipelines** in the left menu.
2. **Create a New Pipeline**:
   - Click **Create Pipeline** and choose **GitHub** as your code source. Log in to GitHub if prompted and authorize access.
   - Select the forked demo project repository you created earlier.
3. **Configure the Pipeline**:
   - In the configuration options, choose **Node.js Express Web App to Linux on Azure**.
   - Review the pipeline steps and understand what each one does for building and deploying your app.
4. **Run the Pipeline**:
   - Click **Run** to initiate the pipeline.
   - For the connection, select **DataCouch**.
   - For **Web App**, select the Azure service you created (`demonodeapp20`).
   - Click **Validate and Configure**.

### Step 5: Set Up Hosted Parallelism for Azure DevOps
If you encounter the error `No hosted parallelism has been purchased or granted...`, follow these steps:

1. **Go to Organization Settings**:
   - In the Azure DevOps portal, click on **Azure DevOps** in the top left.
   - At the bottom left, click on **Organization settings**.
2. **Configure Parallel Jobs**:
   - Select **Parallel jobs** under **Pipelines**.
   - Next to **Monthly purchases for hosted**, click **Change**.
3. **Set Up Billing for Parallel Jobs**:
   - Click **Set up billing**. When the subscription page loads, click **Save**.
   - Set **Paid parallel jobs** to **1** for **MS-hosted** and click **Save**.
   - This setup may take a few minutes to activate; you can grab a coffee in the meantime.
4. **Return to the Pipeline and Run It Again**:
   - Once parallelism is set up (you can only tell by not getting the error), go back to your pipeline in Azure DevOps and click **Run** to trigger it again. 

### Step 6: Grant Permission for the Deployment Phase
During the deployment phase, you may encounter a permission request to access resources.

1. **Grant Permission**:
   - When you see the message "Pipeline needs permission to access a resource," click **View**.
   - Click **Permit** to grant the necessary access for the pipeline to deploy to your Azure Web App.

### Step 7: Verify the Deployment
1. **Check the Azure Portal**:
   - Go to your App Service in the Azure portal.
   - Under **Overview**, you’ll find the URL for your app (e.g., `https://demonodeapp20-blablabla.azurewebsites.net`). Click on it to verify that your application is running.
2. **Review Logs if Needed**:
   - If there are any issues, you can find more details in the deployment logs available in both Azure DevOps and the Azure portal.

You’ve now set up continuous deployment for a Node.js web app on Azure App Service using Azure DevOps. Each time you update the GitHub repository, the pipeline will automatically build and deploy the latest changes to your web app.
