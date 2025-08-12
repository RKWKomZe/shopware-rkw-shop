# ShopwareDDEV-Base

## Requires Docker & DDEV
### Docker Installation
* Docker has to be installed. For installing Docker on Ubuntu see: https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository
* After that you need to install `docker-composer-v2`:
```
apt-get install docker-compose-v2
```
* It is important that the user with whom Docker is to be used is in the Docker group.
```
sudo usermod -aG docker $USER
```
Then check whether the user is now in the group.
IMPORTANT: If not, a restart is probably necessary!
```
groups
```
It should then be possible to call the following command without authorization errors:
```
docker ps -a
```

### DDEV
* For routing with SSL mkcert (https://github.com/FiloSottile/mkcert#installation) has to be installed
```
sudo apt install libnss3-tools
```
* Then we install DDEV (https://ddev.readthedocs.io/en/stable/users/install/ddev-installation/#linux)
```
sudo sh -c 'echo ""'
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://pkg.ddev.com/apt/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/ddev.gpg > /dev/null
sudo chmod a+r /etc/apt/keyrings/ddev.gpg

# Add DDEV releases to your package repository
sudo sh -c 'echo ""'
echo "deb [signed-by=/etc/apt/keyrings/ddev.gpg] https://pkg.ddev.com/apt/ * *" | sudo tee /etc/apt/sources.list.d/ddev.list >/dev/null

# Update package information and install DDEV
sudo sh -c 'echo ""'
sudo apt update && sudo apt install -y ddev
```
* Finally, install the local certificate authority for certificates:
```
mkcert -install
```
* Now add some add-ons we need
```
ddev get ddev/ddev-phpmyadmin
```
## Getting started
- Clone this repository to your local machine.
- Start your containers
```
ddev start
```
- Do a
```
ddev composer install
```
- That's it! Run `ddev status` to see which website-urls you can use.
# How the .env-files work
The process is as follows:

Shopware first loads .env
This is the standard configuration, which is often checked into the repository.

.env.local overwrites .env
This file is intended for your local, private settings (usually in .gitignore).

.env.<APP_ENV> (e.g. .env.prod)
Is read for a specific environment.

.env.<APP_ENV>.local (e.g. .env.prod.local)
Overwrites all previous values specific to this environment.

System environment variables
Everything that DDEV sets in the container as MAILER_DSN, for example, overwrites the .env values.

# Deployment
* Before you deploy add your ssh-keys to your containers to allow access to GIT-repository for deployment
```
ddev auth ssh
```

# Commands for DDEV
- SSH into the web-container
```
ddev ssh
```
- Stop containers
```
ddev stop
```

