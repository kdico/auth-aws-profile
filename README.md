# auth-aws-profile

Make authenticating your AWS credentials with MFA easier by using a script provided in this repository. Developed using
Python 3.9.6 and [Poetry](https://python-poetry.org/). The authentication process uses the V3 SDK for Python.

### Requirements

* Python `^3.6.2`.
* An AWS credentials file, e.g. `~/.aws/credentials`, with one or more sections that contain the following keys.
    * `aws_access_key_id`
    * `aws_secret_access_key`
    * `aws_session_token`
* An AWS configuration file, e.g. `~/.aws/config`, with one or more `[profile *]` sections.
    * The `[profile *]` should reference a section from `~/.aws/credentials` using `source_profile = *` and must have
      the `role_arn` key as well.

### Example

Here's what the script expects your AWS configuration and credentials file to look like.

```
# ~/.aws/config

[default]
region = ap-northeast-1
output = yaml

[profile my-role]
role_arn = arn:aws:iam::123456789012:role/my-role
source_profile = mfa
```

```
# ~/.aws/credentials

[default]
aws_access_key_id = foo
aws_secret_access_key = bar

[mfa]
aws_access_key_id = foo
aws_secret_access_key = bar
aws_session_token = baz
```

The AWS CLI can still find `my-role` even if you move it to `~/.aws/credentials` as long as it's renamed to `[my-role]`
instead of `[profile my-role]`. However, this script requires `my-role` to be in `~/.aws/config` and must be passed to
the script using the complete profile section name, e.g. `profile my-role`.

### Usage

Install the script from PyPi and verify the version.

```
pip install auth-aws-profile
auth-aws-profile --version
```

Here's a simple usage example based on the files mentioned in [Example](#example).

```
auth-aws-profile "profile my-role" "arn:aws:iam::123456789012:mfa/john.doe"
```

See the help documentation for details.

```
auth-aws-profile --help
```

### Development

* At least Python 3.6.2 must be installed in your system.
* [Poetry](https://python-poetry.org/) is installed. See [Installation](https://python-poetry.org/docs/#installation).
* Install the project with Poetry from the root using `poetry install`.
