# puppet-drupal

This module installs Drupal and manages Drupal sites on an Ubuntu Linux system.

## Installation

This module requires at least puppet 3.0. It also has dependencies on other puppet modules from puppet forge. Use librarian-puppet to install it.

Puppetfile:
```shell
forge "https://forgeapi.puppetlabs.com"

mod "jwbraucher/drupal",
  :git => "git@github.com:/jwbraucher/puppet-drupal.git",
  :ref => "latest"
```

Command to install:
```shell
$ librarian-puppet update
```

To test the module locally :
puppet apply --debug --verbose --detailed-exitcodes --hiera_config=./puppet/hiera.yaml 
--modulepath=./puppet/modules:/vagrant-puppet puppet/manifests

## Usage
To use this puppet module, add something like the below to your hiera config:  
(only one site should be enabled at a time)

```shell

# declare drupal module
classes:
  - drupal

# install drupal with drush 
# (only needed for new sites)
drupal::install: no
drupal::mail_domain: example.com
drupal::mail_server: smtp.example.com

# drupal sites
drupal::sites:
  site1.example.com:
    restore: /path/to/drush/archive
    enabled: default

```

