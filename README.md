# aws-utils

### Bash scripts to ease self-managagement for instances on EC2

## IMDSCurl

`IMDSCurl` interacts with the EC2 Instance Metadata Service Version 2 (IMDSv2) in AWS environments. It simplifies metadata retrieval by managing IMDSv2 tokens automatically, caching them securely, and allowing users to query instance metadata as simply as they used to be able to with curl and IMDSv1.

### Why This Script Exists

AWS introduced IMDSv2 to enhance security by requiring a session-oriented approach to accessing instance metadata. This means that every request to the Instance Metadata Service must include a valid session token, which needs to be periodically refreshed. While this improves security, it also complicates scripting and automation that need to interact with the IMDS. 

`IMDSCurl` was created to:

- **Simplify IMDSv2 Interaction**: Automatically manage the generation, caching, and refreshing of IMDSv2 tokens.
- **Provide a `curl`-like Interface**: Allow users to query metadata with minimal changes to their existing workflows.

### Prerequisites

- curl

### Installation

   ```bash
   sudo curl -o /usr/local/bin/IMDSCurl -L https://raw.githubusercontent.com/stevemadere/aws-utils/latest/IMDSCurl && sudo chmod 755 /usr/local/bin/IMDSCurl
   ```
### Example usage

```bash
MY_INSTANCE_ID=$(IMDSCurl latest/meta-data/instance-id)
# or
MY_INSTANCE_ID=$(IMDSCurl http://169.254.169.254/latest/meta-data/instance-id)
```

## associate_this_elastic_ip_address_with_me

`associate_this_elastic_ip_address_with_me` is a bash script that will associate an Elastic IP address with the current instance.  The IP address can be specified numerically or via a hostname and looked up with DNS.

### Prerequisites

- aws-cli
- host command
- jq command
- IMDSCurl command (see above)
- instance IAM Role must have permissions to attach the elastic ip address in question

### Installation

   ```bash
   sudo curl -o /usr/local/bin/associate_this_elastic_ip_address_with_me -L https://raw.githubusercontent.com/stevemadere/aws-utils/latest/associate_this_elastic_ip_address_with_me && sudo chmod 755 /usr/local/bin/associate_this_elastic_ip_address_with_me
   ```


