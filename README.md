# Maneuver 

Maneuver for Laravel 5 with shared hosting asset deployment.

## Installation

1. Add the package to your composer.json file and run `composer update`:

```json
{
	"repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/tech-know/Maneuver"
        }
    ],
    "require": {
        "fadion/maneuver": "dev-assets"
    }
}
```

2. Add `Fadion\Maneuver\ManeuverServiceProvider` to your `config/app.php` file, inside the `providers` array.

3. Publish the package's config with `php artisan vendor:publish`, so you can easily modify it in: `config/maneuver.php`

## Configuration

The first step is to add servers in the configuration file. If you followed step 3 above, you'll find it in `config/maneuver.php`.

Add one or more servers in the `connections` array, providing a unique, recognizable name for each. Credentials should obviously be entered too. Optionally, specify a default server for deployment, by entering the server's name in the `default` option. Changes will be deployed to that server if not overriden. In case you leave the `default` option empty, deployment will be run to all the servers.

Don't forget to set the `scheme` for your servers to either `ftp` or `ssh` for SFTP.

Example Configuration:

	'production' => array(
            'scheme'    => 'ftp',
            'host'      => 'yourdevserver.com',
            'user'      => 'user',
            'pass'      => 'myawesomepass',
            'path'      => '/path/to/server/appname/',
            'port'      => 21,
            'passive'   => true,
            'asset_path'=> '/path/to/public_html/appname/'
        ),

## Asset Deployment

This version's purpose is to allow for assets to be deployed to a separate folder on the remote server. When deploying Laravel applications on a shared hosting server all asset files such as Images, CSS, and Javascripts must be in the public_html/* directory of your shared server. It is recommended that the Laravel application itself be stored in a non public folder such as your root directory. 

And Example shared hosting file structure could look like this:

	.
	+-- /AppName
	|	+-- /app
	| 	+-- /bootstrap
	|	+-- /config
	|	+-- /database
	| 	+-- etc...
	+-- /logs
	+-- public_ftp
	+-- public_html
	|	+-- /AppName
		| 	+-- index.php
		|	+-- images
		|	+-- css
		|	+-- js

This version of Fadion's Maneuver allows you to define an asset folder in the config file and deploy any changes in your local `public` folder to that folder on the server.

#### Usage

	php artisan deploy --assets
