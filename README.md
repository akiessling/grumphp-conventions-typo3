# What does it do

Provides a preconfigured grumphp setup for TYPO3 extensions that i write.   

# Usage

## Install

~~~
composer config repositories.grumphp-conventions-typo3 vcs https://github.com/akiessling/grumphp-conventions-typo3.git
composer require --dev andreaskiessling/grumphp-conventions-typo3 dev-master
~~~

## Setup composer configuration

The configuration currently expects the package in some specific directories. Run these lines to setup composer accordingly. This will only take effect, if you run composer from the extension, not from your project and should thus be safe to use.

~~~
touch .gitignore && echo .Build >> .gitignore && echo composer.lock >> .gitignore
composer config vendor-dir .Build/vendor
composer config bin-dir .Build/bin
composer config extra.typo3/cms.cms-package-dir "{\$vendor-dir}/typo3/cms"
composer config extra.typo3/cms.web-dir .Build/Web
~~~

## Configure grumphp

Create a grumphp.yml in your extension directory and insert this content:
~~~
imports:
  - { resource: .Build/vendor/andreaskiessling/grumphp-conventions-typo3/grumphp.yml }
~~~

## Running it

~~~
.Build/bin/grumphp run
~~~

# Fixing errors reported from slevomat checks:

I could not get the checks to run via phpcs directly due to some autoloading issues, thus they are currently executed through a shell task. To fix the issues, run phpcbf with the given standard:

~~~
`composer config bin-dir`/phpcbf -p --standard=`composer config vendor-dir`/andreaskiessling/grumphp-conventions-typo3/phpcs-slevomat.xml --runtime-set ignore_errors_on_exit 1 --runtime-set ignore_warnings_on_exit 1  Classes
~~~
