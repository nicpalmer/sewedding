## A software engineer's guide to planning a wedding

Welcome to my blog, I very recently got engaged. Give that my background is working with computers I felt that I could use these tools to help plan my wedding. 

### You'll need a server! 

I love terraform, and my current employer don't do a lot of work on the cloud, so I've been itching for a reason to use it again. Natrually, it makes sense to use terraform to build my server. 

#### Terraform (main.tf) 
```
// Token from variables.tf - this is the environment variable TF_VAR_hcloud_token
provider "hcloud" {
  token = "${var.hcloud_token}"
  endpoint = "${var.hcloud_endpoint }"
}

resource "hcloud_server" "jira" {
  name = "${var.name}"
  image = "${var.image}"
  server_type = "${var.server_type}"
}

resource "hcloud_floating_ip" "master" {
  type = "ipv4"
  server_id = "${hcloud_server.jira.id}"
}
```
#### Terraform (variables.tf)

```
// Remember to set this as an enviroment variable
// `export TF_VAR_hcloud_token='<YOUR_TOKEN_HERE>'

variable "hcloud_token" {}

variable "hcloud_endpoint" {
  default = "https://api.hetzner.cloud/v1"
}

variable "name" {
  default = "jira"
}

variable "image" {
  default = "centos-7"
}

variable "server_type" {
  default = "cx21"
}
```


### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/nicpalmer/sewedding/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
