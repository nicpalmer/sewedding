## A software engineer's guide to planning a wedding

Welcome to my blog, I very recently got engaged. Give that my background is working with computers I felt that I could use these tools to help plan my wedding. 

### You'll need a server! 

I love terraform, and my current employer doesn't do a lot of work on the cloud, so I've been itching for a reason to use it again. Natrually, it makes sense to use it to build my server. I really like Hetzner, because they are crazy cheap and hosted in Europe.

A CX21 is 2vCPU, 4GB Ram, 40GB Disk and 20TB Throughput (Per Month) for €5.88, which I think is a great price. 

TODO: Add the code for generating SSH-KEYS to the host for better security. 

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

### Jira

Jira is used by thousands of developers everyday, wedding planners probably not so much. I have seen a few blog posts and tweets about people in a simmilar mindset to me, 

* https://community.atlassian.com/t5/Jira-articles/A-Jira-Wedding-Key-Love/ba-p/830807
* https://twitter.com/Jira/status/668940888597467136

My idea here is that my partner and I can have a solid idea, of what we have to do, when by and how. (my partner especially likes the idea of an approval/review workflow where she can force me to rework things she doesn't like...) 

The workflow looks at little like this;

