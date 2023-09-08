# EC2 Steampipe
[Steampipe](https://steampipe.io/) is an open source tool for querying cloud APIs using SQL. The [AWS plugin](https://hub.steampipe.io/plugins/turbot/aws) maps AWS APIs to over [400 SQL tables](https://hub.steampipe.io/plugins/turbot/aws/tables) that you can query separately or in combination to answer questions about your AWS environment compute, networking, and storage resources, check security posture, explore billing, and more. 

The tool is mentioned on [AWS Open Source blog](https://aws.amazon.com/blogs/opensource/)
- [Querying AWS at scale across APIs, Regions, and accounts](https://aws.amazon.com/blogs/opensource/querying-aws-at-scale-across-apis-regions-and-accounts/)
- [Compliance auditing with Steampipe and SQL](https://aws.amazon.com/blogs/opensource/compliance-auditing-with-steampipe-and-sql/)
- [Dashboards as code: A new approach to visualizing AWS APIs](https://aws.amazon.com/blogs/opensource/dashboards-as-code-a-new-approach-to-visualizing-aws-apis/)
- [Using Steampipe Relationship Graphs to Navigate Cloud Resources on AWS](https://aws.amazon.com/blogs/opensource/using-the-new-relationship-graph-capabilities-in-open-source-steampipe-on-aws/)

[Installing](https://steampipe.io/downloads) steampipe and [configuring](https://hub.steampipe.io/plugins/turbot/aws#get-started) AWS plugin requires effort and may raise security concerns as users must have [ReadOnlyAccess](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/ReadOnlyAccess.html) IAM permission. Windows users must install Windows Subsystem for Linux (WSL 2.0) and Ubuntu.

This repo provides a CloudFormation template that provisions a EC2 instance running [Amazon Linux 2](https://aws.amazon.com/amazon-linux-2/) with Steampipe and AWS plugin installed and configured for immediate use. 


## Getting started
Download the [CloudFormation template](ec2-steampipe.yaml) and provision it in your AWS [CloudFormation console](https://console.aws.amazon.com/cloudformation). 
Once provisioned, go to Outputs section.
![CloudFormation Outputs section](images/outputs.png)

Open the `SSMSessionManager` link value in a new browser tab to start SSM Session Manager session. Use the command `sudo passwd ec2-user` to set login password. 

Open the `DCVwebConsole` link value to access NCIE DCV web browser console and login as user `ec2-user` with the password that you have set. 
 

## Attribution
[Steampipe](https://github.com/turbot/steampipe), [AWS plugin](https://github.com/turbot/steampipe-plugin-aws), [Sqlectron GUI](https://github.com/sqlectron/sqlectron-gui), [Visual Studio Code](https://github.com/microsoft/vscode) and other binaries in the EC2 instance are downloaded without modification. Usage indicates acceptance of their licenses.


## Using Steampipe
Steampipe is installed with AWS plugin configured for the region where CloudFormation template is provisioned. From a terminal session, you can [query](https://steampipe.io/docs/query/overview) your AWS environment. You can run Steampipe in [service mode](https://steampipe.io/docs/managing/service) and connect to it using a Postgres-compatible database client such as [Sqlectron GUI](https://sqlectron.github.io/) or [Visual Studio Code](https://code.visualstudio.com/) (with [PostreSQL](https://marketplace.visualstudio.com/items?itemName=ckolkman.vscode-postgres) extension) which are installed in the EC2 instance. 

![using steampipe](images/ec2-steampipe.png)

Refer to [AWS plugin site](https://hub.steampipe.io/plugins/turbot/aws) for [table definitions and examples](https://hub.steampipe.io/plugins/turbot/aws/tables), and advanced configuration options such as [multi-region](https://hub.steampipe.io/plugins/turbot/aws#multi-region-connections) and [multi-account](https://hub.steampipe.io/plugins/turbot/aws#multi-account-connections) connections.

[Steampipe Hub mods site](https://hub.steampipe.io/mods?q=AWS) has mods that can perform [compliance auditing](https://aws.amazon.com/blogs/opensource/compliance-auditing-with-steampipe-and-sql/) and run [dashboards](https://aws.amazon.com/blogs/opensource/dashboards-as-code-a-new-approach-to-visualizing-aws-apis/) among other functions. 

[Steampipe Blog](https://steampipe.io/blog/) publish useful AWS related posts. Some examples are
- [Tackling Third-Party Risks in your AWS Environment](https://steampipe.io/blog/aws-trusts)
- [Visualizing AWS with Relationship Graphs](https://steampipe.io/blog/aws-relationship-graphs)
- [Secure your Terraform deployments in AWS](https://steampipe.io/blog/codepipeline-scanning)
- [Streamlining incident response investigations with Steampipe relationship graphs](https://steampipe.io/blog/relationships-and-ir)
- [Mapping your AWS attack surface](https://steampipe.io/blog/aws-attack-surface)


## Updating steampipe
To update steampipe and associated plugins, login to EC2 instance and run `/home/ec2-user/update-steampipe` script. 


## About remote web console
Remote web access is provided by [NICE DCV](https://aws.amazon.com/hpc/dcv/) server and supports [file transfer](https://docs.aws.amazon.com/dcv/latest/userguide/using-transfer-web.html). Usage indicates acceptance of [NICE DCV EULA](https://www.nice-dcv.com/eula.html).

![file transfer](https://docs.aws.amazon.com/images/dcv/latest/userguide/images/web-storage.png)

Native clients can be downloaded from https://download.nice-dcv.com/


## EC2 in private subnet
The CloudFormation templates are designed to provision EC2 instances in [public subnet](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Scenario1.html). To use them for EC2 instances in [private subnets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Scenario2.html) with internet connectivity, set `displayPublicIP` parameter value to `No` 




## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.
