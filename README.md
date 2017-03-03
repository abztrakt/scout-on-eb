# scout-on-eb

## Quickstart

Create a directory for your files:

    mkdir myscout-eb
    cd myscout-eb

Clone this repository:

    git clone https://github.com/abztrakt/scout-on-eb.git

Create and activate a virtualenv:

    virtualenv venv
    source venv/bin/activate

Install requirements:

    cd scout-on-eb
    pip install -r local-requirements.txt
    
Authenticate (This is unique to UW federated login, if you're just using an IAM user you can skip this step.)

    awslogin
    
Initialize the eb cli (The saml profile is unique to UW federated login):

    eb init --profile saml
    
Create the eb environment:

    eb create

**Note:** this next bit with the env.config is a little wonky, as you have to stage it in git, but don't ever really want to commit it since it has secrets. There has to be a better way!

(Optional) Copy environment variable configuration and fill in the blanks, other wise you'll use the AWS console to create the environment variables listed in that file:

    cp sample.env.config .ebextensions/env.config
    git add .ebextensions/env.config
    eb deploy --staged
    git reset .ebextensions/env.config
    
