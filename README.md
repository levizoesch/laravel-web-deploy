# laravel-web-deploy
A simple github action script to deploy a laravel application to a FTP host using SSH Key/passphrase

This is a 2 step process to get fully implemented.

This will initialize the files onto the domain from the repository.

```
name: FTP Upload

on:
  push:
    branches:
      - main

jobs:

  web-deploy:

    name: 🎉 Deploy to Production
    runs-on: ubuntu-latest
    steps:
      - name: 🚚 Get latest code
        uses: actions/checkout@v3

      - name: 📂 Sync files
        uses: SamKirkland/FTP-Deploy-Action@v4.3.4
        with:
          server-dir: public_html/
          server: ${{ secrets.FTP_SERVER }}
          username: ${{ secrets.FTP_USERNAME }}
          password: ${{ secrets.FTP_PASSWORD }}
          protocol: ftp
          port: 21
          exclude: |
            **/.git*
            **/.git*/**
            **/docker*/**

```

You will then need to recommit the default file that is in this repository named `laravel-web-deploy.yml`

# Create a SSH Key
Within your environment, create a SSH Key with a passphrase

# Authorize SSH Key
Sometimes you will need to authorize the key, under the Authorization Status you will see its status. Click manage to change.

# Create Deploy Keys
Add your Public SSH Key to your Deploy Keys.
Go to your `Github repository`, `Settings`, `Deploy Keys`

# Create Github Repository Secrets
Go to your `Github repository`, `Settings`, `Secrets & Variables`, Select `Actions` drop down menu. 

SSH_HOST = The IP address

SSH_KEY = The Private SSH Key

SSH_PASS = The SSH Passphrase

SSH_USER = The SSH Username

# Commit the laravel-web-deploy.yml file to your repository.

# If all went well, your application should be set into Maintenance Mode before the FTP Files are uploaded, then the application will be taken out of Maintenance Mode.

# Help, Questions, Need More Context Submit a `New Issue`, or even better a PR...
Lets make development easier for everyone...
