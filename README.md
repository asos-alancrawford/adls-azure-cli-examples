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
`az account set --subscription 'Visual Studio Enterprise'

## Login - SPN
1. 