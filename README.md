aws-role
========

aws-role simplifies getting and using AWS role credentials. 


WARNING: This will rewrite the configuration file specified by AWS_CONFIG_FILE, and add an 'arn' option to each profile you specify. This means any comments you might have put in your config file will be discarded.

To use aws-role, you need to have your AWS configuration file specified in your AWS_CONFIG_FILE environment variable, and that config file (e.g. ~/.aws) needs to have a (1) a working [default] profile, and (2) at least the section header for the the other profiles you want to use. For example, my ~/.aws file looks like:

    [default]
    region = us-east-1
    aws_access_key_id = XXXXXXXXXXXXXXXx
    aws_secret_access_key = XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

    [profile customer1]
    region = us-east-1

    [profile customer2]
    region = us-east-1

Now, to access the customer1 profile, I run:

    $ aws-role customer1
    ARN: arn:aws:iam::XXXXXXXXX:role/CUSTOMERAdmin
    Access Key acquired: XXXXXXXXXXXXXXXXXXXXXx

And then I use the profile with the normal 'aws' commands:

    $ aws --profile customer1 ec2 describe-instances
    "Reservations": [
    ....

Note that I was prompted for the ARN for the role. You only have to enter this one time (it will remember it in subsequent runs).

