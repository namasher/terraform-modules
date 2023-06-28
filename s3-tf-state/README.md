# S3-TF-STATE module

This terraform module is used to create an S3 bucket with versioning enable.
The idea of this module is that it can be used in any project that needs disk
space or as a solution to be used to store your .tfstate files from multiple
modules.

## Backend for terraform

If this module is used as a backend solution for your .tfstate files you will
first need to create it with local storage due to a chicken-egg problem. After
the infrastructure of this module has been created you can transition this
module .tfstate file to your recently created S3 bucket. In order to do so
follow the steps below:

1. Add the following terraform backend block to your copy of the s3-tf-module:

```
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }

  backend "s3" {
    bucket = "mybucket"
    key    = "/"
    region = "us-east-1"
  }

  required_version = ">= 1.2.0"
}
```

2. Run the command below to configure the new backend for this S3 bucket. Your
   tfstate file will be uploaded in the aws bucket.

   ```
   terraform init -migrate-state
   ```
