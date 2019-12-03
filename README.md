# koenhendriks/phpdocker

## Usage

* Docker image is available at [Docker Hub](https://hub.docker.com/r/koenhendriks/phpdocker/).
* The primary goal of this Docker image is custom image for CI, but you can use it like you want.

## Example

### Gitlab CI Example

__Multiversion PHP Unit Test__ 
```yml
phpunit_72:
  image: koenhendriks/phpdocker:7.2
  stage: test
  script:
    - php ./vendor/bin/phpunit --colors=never -c phpunit-runner.xml

phpunit_73:
  image: koenhendriks/phpdocker:7.3
  stage: test
  script:
    - php ./vendor/bin/phpunit --colors=never -c phpunit-runner.xml

# With xdebug coverage
phpunit74:
  image: koenhendriks/phpdocker:7.4
  stage: test
  script:
    - php -d$XDEBUG_EXT ./vendor/bin/phpunit  --coverage-text --colors=never --coverage-clover ./coverage/phpunit.coverage.xml --log-junit ./coverage/phpunit.report.xml
  artifacts:
    expire_in: 1 week
    reports:
      junit: ./coverage/phpunit.report.xml
    paths:
      - ./coverage/
  only:
    - master
    - tags
```

## Tags

* Tags depend on version of PHP included.
* They are given by git branches.
* You can see them at [Docker Hub](https://hub.docker.com/r/koenhendriks/phpdocker/tags/).

---

## Available Bash scripts

## Built-in applications

* [GIT](https://git-scm.com/)
* [PHP](http://php.net) (from official [PHP Docker images](https://registry.hub.docker.com/_/php/))
	* [XDebug](http://xdebug.org)
		* XDebug is not enabled by default, see i.e. [Composer docs](https://getcomposer.org/doc/articles/troubleshooting.md#xdebug-impact-on-composer)
		* You can run script with XDebug enabled like: `php -d$XDEBUG_EXT vendor/bin/phpunit` or `php_xdebug vendor/bin/phpunit`
* [NodeJS](https://nodejs.org)
	* [Yarn](https://yarnpkg.com/)
* [Composer](https://getcomposer.org)
* [PHP_CodeSniffer](https://www.squizlabs.com/php-codesniffer) 
* [PHPUnit](https://phpunit.de)

### PHP

* PHP is started automatically.
* You can type PHP commands, eg. `php -r "echo 1;"`.
* Each Docker image contains ONLY ONE VERSION OF PHP, so:
	* If you need PHP 7.0, use `koenhendriks/phpdocker:7.0`.
	* If you need PHP 7.1, use `koenhendriks/phpdocker:7.1`.
	* If you need PHP 7.2, use `koenhendriks/phpdocker:7.2`.
	* If you need PHP 7.3, use `koenhendriks/phpdocker:7.3`.

### Composer

* Composer is installed globally.
* You can run it, eg. `composer self-update`.

### PHP_CodeSniffer

* PHP_CodeSniffer is installed globally.
* You can run it, eg. `phpcs --standard=PSR2 -nsp src tests`.

### PHPUnit

* PHPUnit is installed globally.
* You can run it, eg. `phpunit  --coverage-text --colors=never --coverage-clover ./phpunit.coverage.xml --log-junit ./phpunit.report.xml`.
