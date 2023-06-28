# terraform-modules
This repository contains terraform modules that can be reused in multiple software projects.

The following instructions apply if you are using macOS as the host OS for terraform

1. Install HomeBrew package manager for macOS. This package manager will help you install terraform CLI
   to be able to control your infrastructure.

    The command below will retrieve the data of the HomeBrew installation script and execute it in a bash
    shell

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

    NOTE: HomeBrew binary may be installed in a non standard location (i.e /opt/homebrew/bin) so a solution
        is to add such path to the PATH system environment variable. Either modifying your .zshrc or running the
        command below:

        export PATH=/opt/homebrew/bin:$PATH

2. Follow the terraform CLI installation instructions for macOS: https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli these are part of the AWS provider but you can use the instructions of another provider since
they should be the same.

3. Set the environment variables for the access keys of your AWS account, so terraform can access you AWS account resources:

    export AWS_ACCESS_KEY_ID=
    export AWS_SECRET_ACCESS_KEY=

4. Terraform will save the infrastructure metadata that you create with any of
   the modules in a file called terraform.tfstate. There are 3 ways you can
   manage such file:
   
   1. If you do not specify a backend in your terraform configuration files the 
   .tfstate file will be saved locally in your host (not recommended).
   
   2. That you use the *s3-tf-state* module to create an S3 bucket to create a
   remote location for the state files, that way you can backup and save them in
   a secure way.

   3. Use terraform cloud or another cloud solution to store the .tfstate file.
    (Keep in mind that only certain backends are supported).

5. Copy the terraform module directory you are interested in adding to your
   project and paste it in your project repository:
    
    cp -R terraform-modules/<module_name> <your-repo>/terraform

6. Run the commands below to create the module's infrastructure so you can use
   it in your project:

    ```bash
    cd <your-repo>/terraform
    ```
    All the definition terraform files have syntax linting however you can run
    this command to make sure the files look readable
    ```bash
    terraform fmt
    ```
    Checks the syntax of the terraform configuration files.
    terraform validate
    Installs the terraform providers under your <your-repo>/terraform 
    directory
    ```bash
    terraform init
    ```
    Creates the infrastructure defined in your module configuration file and
    the .tfstate file will be created in the file backend that you chose
    ```bash
    terraform apply
    ```
