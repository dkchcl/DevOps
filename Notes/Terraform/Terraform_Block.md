## Terraform Block 

terraform
required_version: string
required_providers: map
provider_meta "<LABEL>": map
backend "<BACKEND_TYPE>": map
cloud: map
organization: string | required when connecting to HCP Terraform
workspaces: map | required when connecting to HCP Terraform
tags: list of strings or map of strings
name: string
project: string
hostname: string | app.terraform.io
token: string
experiments: list of strings
