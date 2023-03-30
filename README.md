# EC2 Steampipe
[Steampipe](https://steampipe.io/) is an open source tool for querying cloud APIs in SQL. The [AWS plugin](https://hub.steampipe.io/plugins/turbot/aws) maps the suite of AWS APIs to over 250 SQL tables that you can query separately or in combination, to answer questions about compute, networking, and storage resources, check your security posture, explore billing, and more.

The tool is mentioned on [AWS Open Source blog](https://aws.amazon.com/blogs/opensource/)
- [Querying AWS at scale across APIs, Regions, and accounts](https://aws.amazon.com/blogs/opensource/querying-aws-at-scale-across-apis-regions-and-accounts/)
- [Compliance auditing with Steampipe and SQL](https://aws.amazon.com/blogs/opensource/compliance-auditing-with-steampipe-and-sql/)
- [Dashboards as code: A new approach to visualizing AWS APIs](https://aws.amazon.com/blogs/opensource/dashboards-as-code-a-new-approach-to-visualizing-aws-apis/)

Installing and configuring steampipe requires effort and may raise security concerns as users must have [ReadOnlyAccess](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/ReadOnlyAccess.html) IAM permission and Windows users must install Windows Subsystem for Linux (WSL 2.0).  


This repo provides a CloudFormation template that provisions an EC2 instance with Steampipe and AWS plugin installed and configured for immediate use. 



## Getting started
Download the [CloudFormation template](ec2-steampipe.yaml) and provision it in your AWS console. 
Once provisioned, go to Outputs section.


Use the `SSMSessionManager` link value to change ec2-user password and `RemoteWebConsole` link value to login to graphical desktop in your browser. 

## Attribution
Steampipe [binary](https://steampipe.io/downloads) and [AWS plugin](https://hub.steampipe.io/plugins/turbot/aws#get-started) are downloaded without modification. Usage indicates acceptance of their licenses


## Using Steampipe
Steampipe is installed with AWS plugin configured for the region where CloudFormation template is provisioned. From terminal session, you can query [steampipe](https://steampipe.io/docs/query/overview). Refer to [documentation site](https://hub.steampipe.io/plugins/turbot/aws#get-started) for advanced configuration options (such as multi-region and multi-account connections) and [table definitions & examples](https://hub.steampipe.io/plugins/turbot/aws/tables)

To perform [compliance auditing](https://aws.amazon.com/blogs/opensource/compliance-auditing-with-steampipe-and-sql/) or run [dashboards](https://aws.amazon.com/blogs/opensource/dashboards-as-code-a-new-approach-to-visualizing-aws-apis/), refer to [Steampipe mods site](https://hub.steampipe.io/mods?q=AWS) for installation and other instructions.


## Updating steampipe
To update steampipe and associated plugins, login to EC2 instance and run `/home/ec2-user/update-steampipe` script. 


## About remote web console
Remote web access is provided by [NICE DCV](https://aws.amazon.com/hpc/dcv/) server, and supports [file transfer](https://docs.aws.amazon.com/dcv/latest/userguide/using-transfer-web.html). Usage indicates acceptance of [NICE DCV EULA](https://www.nice-dcv.com/eula.html).

![file transfer](https://docs.aws.amazon.com/images/dcv/latest/userguide/images/web-storage.png)

Native clients can be downloaded from https://download.nice-dcv.com/


## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.
