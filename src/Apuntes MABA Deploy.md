# Apuntes MABA Deploy


### Deploy website to IIS from linux build agent

https://stackoverflow.com/questions/71754411/deploy-website-to-iis-from-linux-build-agent


~~~
#!/usr/bin/bash
SOURCE_FOLDER=/path/to/project/bin/Release/net8.0/publish/win-x64
SITE_NAME="SITE\\path"
# I haven't figured out how to do Kerberos authentication, so just doing basic auth here
USERNAME="iisdeployuser@example.com"
PASSWORD='good-password!@#$'
SERVER_HOSTNAME="iisserver01.example.com"
# If you haven't set up certificates for your Web Deploy endpoint,
# you'll need to skip cert hostname verification
ALLOW_UNTRUSTED_CERTIFICATES="true"

# WebDeploy defaults to listen on port 8172 with HTTPS
ENDPOINT="https://$SERVER_HOSTNAME:8172/msdeploy.axd"

DEST_PARAMS='contentPath="'"${SITE_NAME}"'",ComputerName="'"${ENDPOINT}"'",AuthType="Basic",UserName="'"${USERNAME}"'",Password="'"${PASSWORD}"'"'

msdeploy -verb:sync \
  -source:contentPath=$SOURCE_FOLDER \
  -dest:${DEST_PARAMS} \
  -enableRule:AppOffline \
  -allowUntrusted=$ALLOW_UNTRUSTED_CERTIFICATES

~~~

