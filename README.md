Aim of tbis script is to Automate the installation of gcloud cli.
I have placed this script into a Jamf policy for use in Jamf Self Service, this is because it also requires user authentication.
Authentication assiociated gcloud cli with the correct google account.

#!/bin/bash

#Logged in user
USER=$(stat -f%Su /dev/console)

#Pull installer
curl -s https://dl.google.com/dl/cloudsdk/release/install_google_cloud_sdk.bash | bash /dev/stdin --disable-prompts --install-dir=/Users/$USER/.config

echo "Correcting permissions on gcloud folder"
chown -R $USER:wheel /Users/$USER/.config/gcloud

#Tidy up installer files
rm -rf /Users/$USER/google-cloud-sdk

#Prompt for login
/Users/$USER/.config/google-cloud-sdk/bin/gcloud auth application-default login

exit 0
