---
slug: terraform-guide
date: 2019-12-25
title: 'Terraform Guide'
description: 'Terraform guide to start your journey with infrastructure as code. This blog will guide for some best practices'
published: true
banner: './javier-allegue-barros-C7B-ExXpOIE-unsplash.jpg'
bannerCredit: 'Photo by [Javier Allegue Barros](https://unsplash.com/photos/C7B-ExXpOIE)'
categories:
  ['Terraform', 'Infrastructure As Code', 'DevOps', 'AWS', 'Cloud Computing']
keywords:
  ['Terraform', 'Infrastructure As Code', 'DevOps', 'AWS', 'Cloud Computing']
---

Terraform is an open source tool that allows you to define infrastructure for a variety of cloud providers (e.g. AWS, Azure, Google Cloud, DigitalOcean, etc) using a simple, declarative programming language.

This guide assumes that you have basic idea of terraform. I have taken examples of terraform with AWS provider. Concepts will be similar with other providers as well.

I will be using this repo for explain all examples: [Terraform-examples](https://github.com/cryptic022/terraform-example)

## Always use latest terraform version (Current version is terraform v0.12.x)

We should always pick the latest terraform version. Reason is that sometimes terraform doesn't have backward compatibility. You will always be stuck with chosen version.

## Always use var-file for terraform plan

We should always use var-file for variables. It will be easy to maintain different variables for different environments and modules.There are different methods which can be used for variables like assign string value to var variable, Environment variable, var-file.  
Checkout this guide for all options [Input Variable guide](https://bit.ly/2ZlVAaT)
Checkout this example [Variable Example](https://bit.ly/2s8Mken)

## Manage s3 backend for tfstate files

Whenever we create any resource with terraform (terraform apply), it maintains the state in tfstate file. Try to run [Variable Example](https://bit.ly/2s8Mken). It will create tfstate file in local. If we modify any resource or add, tfstate will be changed after each terraform apply.
In team , multiple team members will be modifing terraform code. So we should maintain tfstate at version control system (Example: S3)
Checkout this example [S3 backend Example](https://bit.ly/2slW0Cf)

## Use dynamo db for locking tfstate modification

Multiple team members will run terraform apply at same time, there could be issues. We should use dynamo db for locking. It will not allow other terraform apply process to change tfstate till release of lock.
Checkout this example [S3 backend Example](https://bit.ly/2slW0Cf)

## Enable version control on terraform state files bucket

First we should use s3 remote storage for managing tfstate. We should enable version control on this s3 remote.
Reason: If any issue comes with current tfstate in production, we can always go back to previous version.
Checkout this example [Variable Example](https://bit.ly/2s8Mken)

## Use terraform import for existing resources

Suppose we have created resources earlier. Now we want to use it with terraform code. It is possible with `terraform import`. It will make these resources as part of terraform.
Checkout this example [Import Example](https://bit.ly/34Vhl2B)

## Use shared modules

Terraform community has shared generic modules on terraform registry like ecs-fargate , ecs-service, s3 bucket creation.  
[Module Registry](https://registry.terraform.io/)
Checkout this example [Share Module Example](https://bit.ly/2ZnNYVi)

## Use terraform modules for mananging different environments(dev/stage/prod)
