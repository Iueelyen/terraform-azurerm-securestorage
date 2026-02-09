Just making my 1st module

Build 3 tf files Main.tf, outputs.tf & variables.tf  
run terraform init
# main.tf  


>terraform {
>  required_version = ">=1.3.7"
>  required_providers {
>    azurerm = {
>      source  = "hashicorp/azurerm"
>      version = "~>3.43.0"
>    }
>  }
>}
>
>locals {
>  tags = {
>    "Environment" = "var.environment",
>    "Project"     = "Terraform Exercise"
>  }
>}
>
>resource "azurerm_storage_account" "securestorage" {
>  resource_group_name           = var.resource_group_name
>  location                      = var.location
>  name                          = var.storage_account_name
>  account_tier                  = "Standard"
>  account_replication_type      = var.environment == "production" ? "GRS" : "LRS"
>  public_network_access_enabled = false
>  tags = local.tags
>
>}

# Variables.tf
>
>variable "resource_group_name" {
>  type = string
>  description = "Resource Group Name"
>}
>
>variable "location" {
>  type = string
>  description = "The Resource Location"
>}
>
>variable "storage_account_name" {
>  type = string
>  description = "The Storage Account Name"
>}
>
>variable "environment" {
>  type = string
>  description = "The Environment either Production or Development"
>}

# outputs.tf
>output "storage_account_id" {
>  value = azurerm_storage_account.securestorage.id
>  description = "The ID of the Secure Storage Account"
>}  
  
# Next things

run terraform fmt  
run terraform validate