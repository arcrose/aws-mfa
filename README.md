# aws-mfa

Authenticate with MFA to AWS and assume a role to get temporary credentials.

## Setup

In order to run this script, you'll need to have Python 2 or 3 installed and
the [boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html)
library installed as well.  You can download it with

```
pip install boto3
```

## Usage

The script accepts two required parameters. The first is a profile name from which
you want to load information about your MFA device and the ARN of the role you
want to assume.

```
aws-mfa profile-name mfa-code
```

**Example**

```
aws-mfa team-prod 123456
```

If you had a `$HOME/.aws/config` file containing something like the following:

```ini
[default]
region = us-west-2

[profile team-prod]
role_arn = arn:aws:iam::000000..00:role/TeamProd
source_profile = default
mfa_seria = arn:aws:iam::00000..00:mfa/user
```

as well as a `$HOME/.aws/credentials` file containing your base user access
key ID and secret key, then invoking `aws-mfa` as above would result in a
successful assumption of the `TeamProd` role.
