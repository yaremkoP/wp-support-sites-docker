# Docker base env setup
### How to setup

1. Install Docker.

2. Clone this repository.

3. Create `.env` file. Look in `.env.example`.
```shell script
cp .env-example .env
```
Edit `WORKSPACE` variable. It is a relative path from Docker config files to folder where contains all legacy sites/repositories on your local machine.

4. Edit `hosts` file. Add sites name and IP to `C:\Windows\System32\drivers\etc\hosts`. Site name is a repositorie names with `.local` ending. **Exaple:**<br/>
`127.0.0.1 johnsdewars_com.local`

5. Copy file `wp-config.php.example` from this repository to `wp-config-local.php` file in each WP repository. Edit file constant `DB_NAME` to valid value. Edit constant `WP_HOME` to the same vaule as in `hosts` file. (Look in `wp-config.php.example`).
```shell script
cp wp-config.php.example /path_to_the_repo/wp-config-local.php
```

6. Run:<br/>
```shell script
docker-compose up -d
```

7. Connect to database, use phpmyadmin http://127.0.0.1:8081 or another sql client (host: 127.0.0.1, port:33066, user and password from `.env` file). Create empty database with the same name as value of constant `DB_NAME` in `wp-config-local.php` file.


### wp-config.php
See `wp-config.php.exapmle`.

### Enadbe xDebug
Create file `docker-compose.override.yml` and insert:
```
version: "3"

services:
  php-fpm:
      environment:
        PHP_XDEBUG: 1
        PHP_XDEBUG_DEFAULT_ENABLE: 1
        PHP_XDEBUG_REMOTE_CONNECT_BACK: 0
        PHP_XDEBUG_REMOTE_HOST: host.docker.internal
```

### Debug in VSCode
Install xDebug extention for Chrome. Copy `.vscode` folder into WP repository. Run 'Listen for XDebug' in VSCode.

### Build theme with npm
Go to the repository. Run (for Windows CMD):
```shell script
docker run --rm --name=npm  -v "%cd%/wp-content/themes/:/usr/src/app" -w="/usr/src/app" -u=node:8 -it node:8 bash
```
##### Byild themes
```shell script
cd theme_name_do_you_need
npm install --no-dev
npm install bower
npm run build
```