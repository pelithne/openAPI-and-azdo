# Introduction
This tutorial contains instruction about how to setup Azure API Management, using ARM templates in Azure DevOps. 

In order to complete this tutorial, you need an Azure Devops account. If you don't have one, you can go  <a href="https://azure.microsoft.com/en-us/services/devops/">here</a>, and select **Start free** for a free account. 

You also need an azure subscription. If you don't have one, create one for free <a https://azure.microsoft.com/en-us/free/">here</a>

## Create new project
To begin with, create a new project in Azure Devops and give it a suitable name, e.g. **APIM CICD with Swagger Import**, and then click **create**

<p align="left">
  <img width="50%" height="50%" hspace="20" src="./media/1-create-new-project.PNG">
</p>
<br>

## Import this repository
To get access to the ARM templates in this repository, you can import them into Azure Devops. There are other ways to do this, but this is an easy way to get going.

Select **Repos**, then look for the section **or import a repository**, and click on the **import** button.

<p align="left">
  <img width="30%" height="30%" hspace="20" src="./media/1-1-import.PNG">
</p>
<br>

In the dialogue that follows, enter the clone url of this repository. In other words https://github.com/pelithne/openAPI-and-azdo.git, and click **import**


<p align="left">
  <img width="50%" height="50%" hspace="20" src="./media/1-2-import-2.PNG">
</p>
<br>


Now that you have the respository with the ARM templates in Azure Devops, you can proceed to create a build pipeline. 


## Create build pipeline
When the project has been created, its time to create a build pipeline. Start by selecting **pipelines** in the left hand panel, and choosing **Builds**.

<p align="left">
  <img width="20%" height="20%" hspace="20" src="./media/2-lefthand-navigation.PNG">
</p>
<br>

In the space that opens, click the button named **New Pipeline**
<p align="left">
  <img width="70%" height="70%" hspace="20" src="./media/3-new-pipelina.PNG">
</p>
<br>


The next space that opens, gives you the option to specify where the code of the project is stored.  

Choose **Use the classic editor to create a pipeline without YAML** at the bottom of the list

<p align="left">
  <img width="50%" height="50%" hspace="20" src="./media/4-where-is-your-code.PNG">
</p>
<br>

In the screen that follows, you should see the repository you recently cloned from github. If you named it as proposed above, it should look something like this:

<p align="left">
  <img width="50%" height="50%" hspace="20" src="./media/7-select-repo.PNG">
</p>
<br>

If it doesn't, make sure that **Azure repos git** is selected as source. When it looks right, select **continue**

In the list that appears, select **start with an empty job**

<p align="left">
  <img width="50%" height="50%" hspace="20" src="./media/8-start-with-empty.PNG">
</p>
<br>

Start by selecting the tab **triggers** and choose to enable continuous integration:
<p align="left">
  <img width="50%" height="50%" hspace="20" src="./media/9-enable-ci.PNG">
</p>
<br>

This is so that a new build process will be started as soon as something is changed in your repository.

Next go to the tasks, and add a Azure Resource Group Deployment task to your build Phase. You do this by clicking the plus sign next to **Agent Job** and writing **azure resource...**  in the search field, like so:

<p align="left">
  <img width="50%" height="50%" hspace="20" src="./media/10-az-rg-deployment.PNG">
</p>
<br>

Select **Azure Resource Gruop Deployment** and click **Add**

After this you need to fill in some details. This is fairly self-explanatory if you have worked with **Azure** before. You need to select which subscription to use, what to call the resource group and which ARM-template to use. The **location** field is simply the geographic location, e.g. **West Europe**

The ARM template to use is ``apim-instance.json``.

Now make sure to set **Deployment mode** to **validation only**. This is because this step is only supposed to be a validation step, that validates the content of the ARM template. Nothing will actually be deployed to the cloud in this step.

After this you can **Save and Queue** the build pipelline.

Finally, we want to make sure that the validated template from this build step is made available to the release pipeleine that we will create next. That is done by creating another job, once again clicking the plus sign next to the **Agent Job**, and then selecting and adding a **Publish Build Artifacts** task.

Leave the defauklt settings, then select **Save and queue**.













