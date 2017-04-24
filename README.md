# Laravel x Guzzle on IBM Bluemix
This repository is used to deploy Website with Laravel Framework and Guzzle on IBM Bluemix

## Get Started
- a. Copy this repository into your Laravel projects. If there are any same files, just copy and replace it. So your structure is going to be like this.
	```
		.bp-config/
		app/
		bootstrap/
		config/ (there is app.php)
		database/
		public/
		resources/
		routes/
		storage/
		tests/
		vendor/
		.cfignore
		.env
		.env.example
		.gitattributes
		.gitignore
		artisan
		composer.json
		composer.lock
		gulpfile.js
		manifest.yml
		package.json
		phpunit.xml
		README.md
		server.php
	```
- b. Change manifest.yml. Attention: YOUR_KEYS can you see with command: php artisan key:generate on your local Laravel directory.
	```
		applications:
		- path: .
		  memory: 128M
		  instances: 1
		  domain: mybluemix.net
		  name: YOUR_APP_NAME
		  host: YOUR_APP_HOST_NAME
		  buildpack: https://github.com/cloudfoundry/php-buildpack
		  disk_quota: 1024M
		  timeout: 60
		  env:
			APP_ENV: production
			APP_DEBUG: false
			APP_KEY: YOUR_KEYS
			CF_STAGING_TIMEOUT: 15
			CF_STARTUP_TIMEOUT: 15
	```
- c. Check your composer.json, if there are are different version (PHP, Laravel, or Guzzle), please change it. For guzzle, please check "Version Guidance" on https://github.com/guzzle/guzzle (see the README file) for matching PHP version and Guzzle version.
	```
		"require": {
			"php": ">=5.6.0",
			"laravel/framework": "5.4.15",
			"guzzlehttp/guzzle": "6.0"
		}
	```
- d. FYI, From this code (composer.json), we know that you dont need any .env files (on Bluemix), because composer.json will duplicate this file and rename the env.example into .env (on Bluemix), but remember, .env files must be exist on your local directory.
	```
		"scripts": {
        "post-root-package-install": [
            "php -r \"copy('.env.example', '.env');\""
        ],
	```
- e. Change .env(for your local) and env.example(for bluemix configuration). Just change the APP_KEY (php artisan key:generate) and APP_URL.
	```
		APP_ENV=local
		APP_KEY=base64:bLfZur5ty0cAN94Jk4FUjh4RcgnRp8PQBslqprbpQZs=
		APP_DEBUG=false
		APP_LOG_LEVEL=debug
		APP_URL=https://example.mybluemix.net/

		DB_CONNECTION=mysql
		DB_HOST=127.0.0.1
		DB_PORT=3306
		DB_DATABASE=homestead
		DB_USERNAME=homestead
		DB_PASSWORD=secret

		BROADCAST_DRIVER=log
		CACHE_DRIVER=file
		SESSION_DRIVER=file
		QUEUE_DRIVER=sync

		REDIS_HOST=127.0.0.1
		REDIS_PASSWORD=null
		REDIS_PORT=6379

		MAIL_DRIVER=smtp
		MAIL_HOST=mailtrap.io
		MAIL_PORT=2525
		MAIL_USERNAME=null
		MAIL_PASSWORD=null
		MAIL_ENCRYPTION=null

		PUSHER_APP_ID=
		PUSHER_APP_KEY=
		PUSHER_APP_SECRET=
	```
- f. Cut and replace "app.php" file into your config folder.

## If you're not using Guzzle you can delete guzzle command on composer.json (each line that call guzzle).