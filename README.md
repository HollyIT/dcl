# DCL
  DCL (docker-compose-laravel) is a modified docker-compose workflow for Laravel, based off of the excellent work by [Andrew Schmelyun](https://github.com/aschmelyun/docker-compose-laravel)

  Note that while this was made for Laravel, it also works fine for non-laravel
  projects, so long as you override the nginx config file to set your
  public html root. 

## Usage

Clone this repository and copy the .env.example file to .env. The .env file contains defaults, which should work for most projects, but feel free to edit.

The following is the available environment variables


|Varaible  |Default  |Description  |Dev  |
|---------|---------|---------|---------|
|PHP_VERSION     |8.2         | Set the PHP version (8.0, 8.1, 8.2)        |         |
|UID     |1000         |User ID to run the container as         |         |
|GID     |1000         |User GID to run the container as         |         |
|NGINX_PORT     |80         |Port to expose Nginx on         |         |
|DB_ROOT_PASSWORD     |password         |Password for root access to database         |         |
|XDEBUG     |false         |Install the latest XDebug extension         |         |
|NODE_VERSION     |current         |Version of Node to install         | Y        |
|DB_EXPOSED_PORT     |3306         |Expose database on this port         |Y         |
|VITE_PORT     |5173         |Port for the vite server         |Y         |


You can review the docker-compose file for any other services you might want to enable. Simple go in and uncomment those services.

The following services are available:
|Service  |Description  |Dev Only|
|---------|---------|------------|
|nginx     | Web server        |            |
|app     |  The actual app/php server       |            |
|db     | Current MySQL version server         |            |
|npm     | NodeJS server        | Y            |



There is a docker-compose.dev.yml with developer options. If you wish to use that, copy it to docker-compose.override.yml.

To create a new project either clone or download this repo. Inside the directory run:

`composer create-project laravel/laravel src`

## DC helper

For starting, stopping, building and all other Docker related stuff, there is a script in the root directory called dc. 

Typing ./dc help in the root directory will list all of the commands. You can also run composer, npm and artisan from the ./dc file.

The current ./dc commands are:


|Command  |Description  |Example  |
|---------|---------|---------|
|help     |  Show help       |./dc help        |
|start    |Start all containers   |./dc start         |
|stop     |Stop all containers         |./dc stop         |
|restart     |Restart all containers         |./dc restart         |
|shell  {container}   |Shell into container        |./dc shell php         |
|artisan ...     |Run an artisan command in the container         |./dc artisan serve         |
|composer ...     |Ran a composer command in the container         |./dc composer install         |
|npm ...     |Run an npm command in the container        |./dc npm install         |
|npx ...     |Run an npx command in the container         |./dc npx run         |
|logs {container}    |View logs of {container}         |./dc logs php         |

All other commands passed to DC will be forwarded to docker-compose.

** NOTE: The DC file loads environment variables from .env and src/.env. Be sure to use ./dc instead of docker-compose so your environment is always set.

## Extra configuration

In config/php you'll find a php.ini file that is loaded last when PHP parses config. You can override anything you need in there. 

## Future development

This was created as a way for me to quickly fire up new Laravel docker-compose projects that can be ran in production or dev, and with a simple wrapper script
to easily run commands and manage all services.

If you feel there is anything missing, please feel free to create a PR and
I'll investigate. That said, I'm sure this will grow over time. I just got
tired of copying and pasting configurations all the time.