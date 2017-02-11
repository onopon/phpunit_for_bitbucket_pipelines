PHPUnit for Bitbucket Pipelines
====

This is a Dockerfile for bitbucket pipelines.
PHP, PHPUnit, Mysql and Composer are included in this.

For example using laravel:

bitbucket-pipelines.yml

```yml
image: onopon/phpunit_for_bitbucket_pipelines
pipelines:
  default:
    - step:
      script:
        - service mysql start
        - sudo -u testuser composer install
        - mysql -u root -p root -e  "CREATE DATABASE xxxx default character set utf8";
        - php artisan migrate
        - phpunit ./tests/
```

## Description

* In the initial state, mysql is stopped. so you should start before using.
* `testuser` is present in Docker. Default user is `root`, and `composer install` should not call with root. So, you can call with testuser.
* This Docker build is present in Dockerhub. https://hub.docker.com/r/onopon/phpunit_for_bitbucket_pipelines/
