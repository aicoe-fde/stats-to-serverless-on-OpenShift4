# Deployment instructions

## For RHPDS

**NOTE**:  This workshop is _not yet available_ in the RHPDS catalog.  Stay tuned for an easier way to do things!

**NOTE**: Make sure your ansible version is >= 2.11

To run this lab in RHPDS, first provision an OpenShift 4 workshop from the RHDPS catalog.  Requesting a Let's Encrypt certificate will make your life easier.  Once the environment is up and running, you'll get an email from RHPDS with the system GUID, bastion hostname, and so on.  The rest of these steps assume you're in this directory of a checkout of this repo.

1.  Log in to the bastion host, following the instructions in the email.
1.  Add an `authorized_keys` file.  If you have a GitHub account with an ssh key, you can do it like this, assuming `${YOUR_GITHUB_HANDLE}` is your GitHub username:  
        `mkdir -p .ssh`  
        `chmod 700 .ssh`  
        `curl https://github.com/${YOUR_GITHUB_HANDLE}.keys >> .ssh/authorized_keys`   
1.  Log out from the bastion host.
1. `export RHPDS_GUID=city-1234`, where `city-1234` is your RHPDS cluster GUID;
1. `export RHPDS_USER=yourkrb-redhat.com`, where `yourkrb` is your Kerberos ID;
1. `export RHPDS_USER_COUNT=5` (or more if you're running an actual workshop)
1. `cd deploy`
1. `./deploy.sh`

`deploy.sh` will attempt to infer the right domain name for your RHPDS cluster based on your cluster GUID and your ssh known hosts file.  If this fails, you'll need to explicitly set the RHPDS domain name with `export RHPDS_DOMAIN=example.opentlc.com`, `export RHPDS_DOMAIN=open.redhat.com`, or something else as appropriate, depending on which domain RHPDS is using (see the email).

Allow ninety minutes or so for the workshop roles to deploy.  Once they're up, you can go through the workshop at your own pace!
