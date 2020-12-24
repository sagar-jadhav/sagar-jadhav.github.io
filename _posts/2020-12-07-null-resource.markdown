---
layout: post
title:  "Executing Shell Script in Terraform via Null Resource"
date:   2020-12-07
categories: [terraform]
---

![Executing Shell Script in Terraform via Null Resource](https://raw.githubusercontent.com/sagar-jadhav/sagar-jadhav.github.io/master/static/img/_posts/terraform_null_resource.png)

Null Resource in Terraform implements all the lifecycle methods as compare to other resources but it doesn't take any action. It is very useful for many use cases but in this blog I will cover How can I use Null Resource to execute the shell script by using local exec provisioner during provision.

### Use Case
Let say I am deploying some resources on private cloud (x-cloud) through terraform but provision should only start when x-cloud is up & running. x-cloud exposed a `REST` API for health check, Hence as part of provisioning I should first check whether x-cloud is up & running, If it is running then continue with the provisioning otherwise stop the provisioning.

#### Step 1: Shell script to perform health check

healthcheck.sh

```
#!/bin/sh

result=$(curl -X GET --header "Accept: */*" "https://jsonplaceholder.typicode.com/todos/1" | jq -r '.id')

if [ $result -eq 1 ]
then
   exit 0
else
   exit 1
fi
```

#### Step 2: Terraform file for provision

main.tf

```
terraform {
  required_version = "> 0.8.0"
}

resource "null_resource" "health_check" {

 provisioner "local-exec" {
    
    command = "/bin/bash healthcheck.sh"
  }
}
```

#### Step 3: Initializing Terraform

```
terraform init
```

**Output:**
```
Initializing provider plugins...

The following providers do not have any version constraints in configuration,
so the latest version was installed.

To prevent automatic upgrades to new major versions that may contain breaking
changes, it is recommended to add version = "..." constraints to the
corresponding provider blocks in configuration, with the constraint strings
suggested below.

* provider.null: version = "~> 2.1"

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

#### Step 4: Provisioning resources

```
terraform apply
```

**Output:**
```
An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # null_resource.health_check will be created
  + resource "null_resource" "health_check" {
      + id = (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

null_resource.health_check: Creating...
null_resource.health_check: Provisioning with 'local-exec'...
null_resource.health_check (local-exec): Executing: ["/bin/sh" "-c" "/bin/bash healthcheck.sh"]
null_resource.health_check (local-exec):   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
null_resource.health_check (local-exec):                                  Dload  Upload   Total   Spent    Left  Speed
null_resource.health_check (local-exec):   0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
null_resource.health_check (local-exec):   0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
null_resource.health_check (local-exec): 100    83  100    83    0     0    154      0 --:--:-- --:--:-- --:--:--   154
null_resource.health_check: Creation complete after 0s [id=9103842202970100490]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

### References:
- [Null Resource](https://www.terraform.io/docs/providers/null/resource.html)
- [Local Exec](https://www.terraform.io/docs/provisioners/local-exec.html)