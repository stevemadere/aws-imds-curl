# aws-utils

### Bash script to ease self-managagement for instances on EC2

Several utilities that make management of AWS resources from an EC2 instance much simpler.
All wrapped up in a single shell script that can be invoked with various subcommands to achieve
varoius purposes.

### Prerequisites

- aws CLI
- curl
- jq

### Installation

   ```bash
   sudo curl -o /usr/local/bin/aws-utils -L https://raw.githubusercontent.com/stevemadere/aws-utils/latest/aws-utils && sudo chmod 755 /usr/local/bin/aws-utils
   # optional
   aws-utils install-commands

   ```
## Invocation

```bash
aws-utils subcommand args

# e.g.
MY_INSTANCE_ID=$(aws-utils IMDSCurl /latest/meta-data/instance-id)
aws-utils associate_this_elastic_ip_address_with_me elastichost.mydomain.com

```


Or, if you have run the **install-commands** subcommand, you can invoke the subcommands as if they are stand-alone scripts:

```bash
# e.g.
MY_INSTANCE_ID=$(IMDSCurl /latest/meta-data/instance-id)
```

## Subcommands

### IMDSCurl

`IMDSCurl` interacts with the EC2 Instance Metadata Service Version 2 (IMDSv2) in AWS environments. It simplifies metadata retrieval by managing IMDSv2 tokens automatically, caching them securely, and allowing users to query instance metadata as simply as they used to be able to with curl and IMDSv1.

### Why This Subcommand Exists

AWS introduced IMDSv2 to enhance security by requiring a session-oriented approach to accessing instance metadata. This means that every request to the Instance Metadata Service must include a valid session token, which needs to be periodically refreshed. While this improves security, it also complicates scripting and automation that need to interact with the IMDS. 

`IMDSCurl` was created to:

- **Simplify IMDSv2 Interaction**: Automatically manage the generation, caching, and refreshing of IMDSv2 tokens.
- **Provide a `curl`-like Interface**: Allow users to query metadata with minimal changes to their existing workflows.

### Example usage

```bash
MY_INSTANCE_ID=$(aws-utils IMDSCurl latest/meta-data/instance-id)
# or
MY_INSTANCE_ID=$(aws-utils IMDSCurl http://169.254.169.254/latest/meta-data/instance-id)
```

## associate_this_elastic_ip_address_with_me

`associate_this_elastic_ip_address_with_me` is a bash script that will associate an Elastic IP address with the current instance.  The IP address can be specified numerically or via a hostname and looked up with DNS.

### Further Prerequisites

- host command (from bind-utils on Amazon linux)
- instance IAM Role must have permissions to attach the elastic ip address in question

### Example usage

   ```bash
   aws-utils associate_this_elastic_ip_address_with_me 35.19.43.12
   # or
   aws-utils associate_this_elastic_ip_address_with_me www.mydomain.com
   ```


