# azure-bbw-poc-api-aks
This project contains an Express.js app that searches the Salesforce demo Apparel API and returns a JSON payload containing the results, to be packaged in a container image, deployed as a Kubernetes service in an Azure Kubernetes Service cluster, and put behind an Azure API Management Service API.

The bulk of the Azure resource allocation is automated by the stand-up-poc-resources.sh script, which requires the Azure CLI to be installed and has a step (to create an AKS cluster) that requires Owner role in the target Azure subscription. This script is meant to be run only once to create several persistent Azure resouces.  Comments in the script provide more insights.  Remember, this
project is a proof of concept from which to learn.  It is not production-worthy as-is.

When you're ready, try running (bash example) `./stand-up-poc-resources.sh 2>&1 | tee logfile` so that you can capture all output and errors to logfile but still see and respond to the script's prompts for input.

The core functionality of the Express.js app derives from concepts and sample code provided in the Salesforce documents [Get Started with the B2C Commerce API|https://developer.salesforce.com/docs/commerce/commerce-api/guide/get-started.html] and [Quick Start: B2C Commerce API and SDK|https://developer.salesforce.com/docs/commerce/commerce-api/guide/api-and-sdk-demo.html]. The POC code to search the SF demo Apparel API is a stand-in for future code that will accesses and orchestrate other SF APIs and is NOT the primary deliverable of the POC. The Azure resource automation examples, the example Helm chart to deploy a Kubernetes service, and the Jenkins build/deploy/test automation examples are the primary deliverables.

There are also example GitHub workflows in this project that automate 1) the build/deploy of the app that provides the API search operation and 2) the regression testing (loosely) of the API search operation.  These workflows demonstrate some basic essentials that could mature into a full CI/CD pipeline over time using [GitHub Actions|https://github.com/features/actions]. These have been superceded by the Jenkins automation that was added subsequently.

Regarding AKS set-up and deployment, see [Quickstart: Develop on Azure Kubernetes Service (AKS) with Helm](https://learn.microsoft.com/en-us/azure/aks/quickstart-helm?tabs=azure-cli.)
- Get access to an Azure subscription with an account that has the Contributor role so you can create and destroy the subsequent resources in isolation.
- Create an Azure Resource Group.
- Create an Azure Container Registry using the Azure CLI.
- Create an AKS cluster using the Azure CLI.
- Build and push the app to the ACR using the CLI.
- Create a Helm chart for the app.
- Run the Helm chart to deploy the app to the AKS cluster using the Azure CLI and Helm.
- Test/demo it.

See also [Use Azure API Management with microservices deployed in Azure Kubernetes Service](https://learn.microsoft.com/en-us/azure/api-management/api-management-kubernetes)