# IMDSCurl

`IMDSCurl` is a bash-based utility designed to interact with the EC2 Instance Metadata Service Version 2 (IMDSv2) in AWS environments. The tool simplifies metadata retrieval by managing IMDSv2 tokens automatically, caching them securely, and allowing users to query instance metadata using a straightforward command-line interface. The tool behaves similarly to `curl` for querying metadata but adds the convenience of handling IMDSv2's token requirements.

## Why This Script Exists

AWS introduced IMDSv2 to enhance security by requiring a session-oriented approach to accessing instance metadata. This means that every request to the Instance Metadata Service must include a valid session token, which needs to be periodically refreshed. While this improves security, it also complicates scripting and automation that need to interact with the IMDS. 

`IMDSCurl` was created to:

- **Simplify IMDSv2 Interaction**: Automatically manage the generation, caching, and refreshing of IMDSv2 tokens.
- **Provide a `curl`-like Interface**: Allow users to query metadata with minimal changes to their existing workflows.

## Installation

You can easily install `IMDSCurl` directly from the GitHub repository using `curl`. Follow the instructions below:

1. **Download the Script**:
   Use `curl` to download the latest version of the script and save it to a location in your system's `$PATH`, such as `/usr/local/bin`.

   ```bash
   sudo curl -o /usr/local/bin/IMDSCurl -L https://github.com/stevemadere/aws-imds-curl/blob/latest/IMDSCurl && sudo chmod 755 /usr/local/bin/IMDSCurl

