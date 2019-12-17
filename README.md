# Docker base env setup
### How to setup

1. Install Docker.

2. Clone this repository.

3. Create `.env` file. Look in `.env.example`.
```shell script
cp .env-example .env
```

4. Edit `hosts` file. Add all repositorie names to this file with `.local` ending. **Exaple:**<br/>
`127.0.0.1 johnsdewars_com.local`

5. Edit `wp-config.php` file in repository.

6. Run:<br/>
```shell script
docker-compose built
docker-compose up -d
```

### wp-config.php
See `wp-config.php.exapmle`.