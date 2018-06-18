# lemp-cloud-init

> Spin up a new Ubuntu, Nginx, MariaDB, PHP server on Digital Ocean

### Notes

* Placeholder values are delimited with `__double_underscores__`

### Instructions

### Getting started

1) Clone this repo

```bash
git clone https://github.com/thegreatsunra/lemp-cloud-init.git
```

2) [Generate an SSH key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) if you don't have one already

```bash
ssh-keygen -t rsa -b 4096 -C "email@domain.tld"
```

3) Copy your SSH key [to your clipboard](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)

```bash
pbcopy < ~/.ssh/id_rsa.pub
```

4) Open `./scripts/cloud-init.sh.txt` in a text editor and replace the placeholder SSH key (around line 30) with the contents of your clipboard

```bash
      - ssh-rsa AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== __email@domain.tld__
```

Be careful not to delete the indentation or `- ` at the beginning of the line, as `cloud-init` needs them to recognize the command

5) Search within `./scripts/cloud-init.sh.txt` and replace the following placeholder strings with your desired values:

* `__username__` - the username of the primary admin user that will be created on the server (e.g. `dane`)
* `__full_name__` - the full name of the primary admin user (e.g. `Dane Petersen`)
* `__email@domain.tld__` - the email address of the primary admin user
* `__domain.tld__` - the domain for your website that will be hosted by nginx (e.g. `thegreatsunra.com`)
* `__temporary_password_change_me_immediately__` - a temporary, throwaway password that will live forever on your server in your `cloud-init` script and **you will immediately change upon logging into the server**

6) Save `./scripts/cloud-init.sh.txt`, select all, and copy it to your clipboard

#### Digital Ocean

1) Log in to Digital Ocean

2) Create a new droplet

3) Under "Select additional options" check the box for "User data" and paste in the contents of `./scripts/cloud-init.sh.txt`

4) Click "Create" and wait a few moments as Digital Ocean creats your new droplet

5) Once Digital Ocean finishes creating your droplet, copy the IP address for your droplet

#### Prepare manual commands

1) Open `./scripts/manual-commands.sh.txt` in a text editor

2) Perform a search-and-replace on `./scripts/manual-commands.sh.txt`, and replace the following values with the values you used in your `cloud-init` script, and the values provided by Digital Ocean when creating your droplet

* `__REPLACE_THIS_TEXT_WITH_YOUR_ACTUAL_SERVER_IP__` - the IP address Digital Ocean assigned to your server
* `__REPLACE_THIS_TEXT_WITH_YOUR_ACTUAL_USERNAME__` - the username of the primary admin user that you created on the server (e.g. `dane`)
* `__REPLACE_THIS_TEXT_WITH_YOUR_ACTUAL_EMAIL__` - the email address of the primary admin user
* `__REPLACE_THIS_TEXT_WITH_YOUR_ACTUAL_DOMAIN__` - the domain for the website that you will host on your server (e.g. `thegreatsunra.com`)
* `__REPLACE_THIS_TEXT_WITH_YOUR_ACTUAL_SERVER_DOMAIN_NAME__` - the domain you want to assign to your server (e.g. `swearengen.thegreatsunra.com`)

3) Save `./scripts/manual-commands.sh.txt`

#### SSH

1) SSH into your new server using the username you chose and the IP address provided by Digital Ocean

```bash
ssh username@ip.address.of.server
```

2) Go line-by-line through `./scripts/manual-commands.sh.txt`, pasting each command into the Terminal to run it on your server like some kind of animal

## License

The MIT License (MIT)

Copyright (c) 2017-2018 Dane Petersen
