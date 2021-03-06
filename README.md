
# Density

[![Build Status](https://travis-ci.org/adicu/density.svg?branch=master)](https://travis-ci.org/adicu/density)


Density is a project to provide easy access to the Wireless Density data from Columbia.
For more details on the project, please view the [spec](SPEC.md).




## Local Dev

This is the recommend means of setting up Density for development.
Next, install [vagrant](http://www.vagrantup.com/).
Once vagrant is installed, you can run `vagrant up`, and vagrant will provision the virtual machine for you.

To start, log into vagrant by following the these steps:

```bash
vagrant ssh
cd /vagrant
source config/settings.dev
```

To run the app after you've logged into vagrant, follow these steps:

```bash
cd density
python density.py
```

To access the database after you've logged call:

`sudo -u postgres psql density`

The data table is under the name `density_data`

[Click here for the PostgeSQL tutorial](http://www.postgresql.org/docs/8.0/static/tutorial.html)


## Importing Dev Data

We use a partial dump of our data for quick-and-easy development.
This gets loaded on VM provision by our Vagrant setup scripts.
It contains a small subset and is not updated frequently, but is sufficient for most feature development and bug squashing.

Be sure to also insert the [Oauth table](config/oauth_dev_dump.sql) so that you can make authenticated requests against the API.






## Docker

The Docker container requires that either the port for the Postgres instance is forward or that the host is set to an exact IP or domain.

Using Docker:

```bash
# enter the project directory
cd density

# builds a Docker image
#   -t dictates that the image is tagged as 'density'
docker build -t density .

# runs a docker container tagged as 'density'
#   --net=host forwards all ports from the host to the container
#       this allows docker to access the Postres port, 5432
#   -e allows setting environment variables within the container
#   -d detaches the process and runs the container like a daemon
docker run --net=host -d density

# ps shows all docker containers currently running
docker ps
```

Running Density within Docker relies on an instance of Consul being run on `localhost:8500` which is used to configure the settings.





## Consul

[Consul](https://consul.io/) is a distributed key/value store that we are using to configure Density in production.
You should not need to intereact with Consul unless you are attempting to deploy it.

Consul is installed within the Vagrant VM automatically.
It can be started with the script at `config/run_consul.sh`.
The web UI is located at [port 8500](http://localhost:8500).








## Routes

Supported routes currently include:

```
/       : Density homepage with "fullness" graphic
/latest : APi endpoint providing the latest data available
/home   : future API homepage that allows a user to obtain an API token
```




## Data Sources

Data for density is provided by CUIT in coordination with ESC.




## Style guide

Make sure to conform to [AirBnb's brilliant style guide](https://github.com/airbnb/javascript) when writing javascript.

# app structure

```
|-- config/ (config settings and install scripts)
|-- README.md (This file)
|-- density/
    \
    |-- density.py  (the executable for this application)
    |-- static/     (your static files, such as js, css, imgs)
    |-- tests/      (unittest scripts that should be used during development)
```



# Changelog

0.1.1: Datetime formatting changed to ISO 8601.
0.1.0: Basic API up and stable.




# List of Developers

- Brian Zeng
- David Hao
- Sungwoo Bae
- Nate Brennand
- Benjamin Low
- Jessica Forde
- Jessica Valarezo
- Maclyn Brandwein
- Jackie Ho
- Dan Schlosser
- Terra Blevins
- Evan Tarrh
- Raymond Xu
- Connie Zhang
