# Sample ASP.NET Core application for GitHub Actions

For all samples to set up GitHub workflows, see [Create your first workflow](https://github.com/Azure/actions-workflow-samples

For more information on building .NET Core applications, see [.NET Core](https://docs.microsoft.com/azure/devops/pipelines/languages/dotnet-core?view=azure-devops).

# Steps to create an End-to-End CI/CD Workflow

## Pre-requisites
* Create a new Web App in Azure Portal with runtime stack as .NETCore and OS as Linux/Windows
* Copy Publish Profile Settings of the app

## Configure secrets in the GH repo:
* In the GH repo with Application code, [Define a new secret](https://github.com/Azure/actions-workflow-samples/blob/master/assets/create-secrets-for-GitHub-workflows.md) under repository by navigating to **settings** > **secrets** > **Add a new secret** 
* Paste the contents for the downloaded publish profile file into the secret's value field
* Now in the workflow file in your branch: `.github/workflows/workflow.yml` replace the secret for the input `publish-profile:` of the deploy Azure WebApp action

## test your workflow
* Commit a change in the app code. For example introduce a text change in the [index file](https://github.com/bbq-beets/ignite/blob/ActionsDemo/Views/Home/Index.cshtml).
* You should see a new GitHub Action initiated in **Actions** tab.
* At the end of the execution, navigate to the App URL to visualise the change introduced.

## Workflow YAML explained

* [Checkout](https://github.com/actions/checkout) Checks out your Git repository content into Github Actions agent.
* Environment setup using [Setup DotNet](https://github.com/actions/setup-dotnet) - Sets up a dotnet environment by optionally downloading and caching a version of dotnet by SDK version and adding to PATH .
* DotNet Build & Publish
* Deploy to App service using azure/webapps-deploy@v1 action which authenticates using [Azure Web App Publish Profile](https://github.com/projectkudu/kudu/wiki/Deployment-credentials#site-credentials-aka-publish-profile-credentials)
which we configured using the secret set up at the repo level


# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

# Legal Notices

Microsoft and any contributors grant you a license to the Microsoft documentation and other content
in this repository under the [Creative Commons Attribution 4.0 International Public License](https://creativecommons.org/licenses/by/4.0/legalcode),
see the [LICENSE](LICENSE) file, and grant you a license to any code in the repository under the [MIT License](https://opensource.org/licenses/MIT), see the
[LICENSE-CODE](LICENSE-CODE) file.

Microsoft, Windows, Microsoft Azure and/or other Microsoft products and services referenced in the documentation
may be either trademarks or registered trademarks of Microsoft in the United States and/or other countries.
The licenses for this project do not grant you rights to use any Microsoft names, logos, or trademarks.
Microsoft's general trademark guidelines can be found at http://go.microsoft.com/fwlink/?LinkID=254653.

Privacy information can be found at https://privacy.microsoft.com/en-us/

Microsoft and any contributors reserve all others rights, whether under their respective copyrights, patents,
or trademarks, whether by implication, estoppel or otherwise.
