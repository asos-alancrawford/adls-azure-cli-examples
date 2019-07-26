# adls-azure-cli-examples
Example commands to assist management of ADLS accounts, folders and files

## Overview
Using Azure CLI is helpful when working with Azure Data Lake Storage to view and manage files and folder structure and provides the ability to do this under the context of either your own credentials or those of a SPN.  Using a SPN is helpful in cases where you need to troubleshoot permissions on folders for automated processes such as CI/CD pipelines, ADF pipelines, etc.

## Pre-requisites
1. Azure CLI
2. An ADLS account which your AAD account has reader or higher permissions for
3. A SPN with reader or higher permissions

## Login - AAD Account
1. Log in using your own AAD account

    `az login`

2. Set the context of the session to the subscription containing the ADLS account you wish to view

    `az account set --subscription 'Visual Studio Enterprise'`

## Login - SPN
1. Find the tenant and application IDs for the subscription you are accessing
    Log in using your own credentials and switch the context to the subscription containing the ADLS account you wish to access by following the previous steps.  To see the tenant ID and app ID run:

    `az ad sp list --display-name <your SPN display name> --query '[].{"id":"appId", "tenant":"appOwnerTenantId"}'`

2. Log in to Azure CLI under the context of the SPN (it is assumed you have a valid client secret for the SPN)

    `az login --service-principal --username <your application id> --password <your app client secret> --tenant <your tenant id>`

## List files
1. Enter the following to return a full list of the file details at the root path within an ADLS account:

    `az dls fs list --account <your adls account name> --path /`

2. List files in a specific path:

    `az dls fs list --account <your adls account name> --path /somepath`

3. Use a JMES query string to return only specific fields from the resultset:

    `az dls fs list --account <your adls account name> --path /somepath --query '[].{"name":"name", "type":"type"}'`

4. Format the results as a table (default is JSON but other options are jsonc, yaml, tsv):

    `az dls fs list --account <your adls account name> --path /somepath --output table`