# Docker Login

* OS: Ubuntu 16.04+

A role that uses the Ansbile module `docker_login` in order to login to Docker-Hub prior to pushing or pulling images
A when condition will determine which login type to use.

```ansible
when: amazon_ecr_login
--OR--
when: username.username is search(docker_username) and not amazon_ecr_login
```

## Requirements

The below requirements are needed on the host that executes this role  
> Note: the requirements stem from the module `docker_login`

    python >= 2.6
    docker-py >= 1.7.0
    Please note that the docker-py Python module has been superseded by docker (see here for details). For Python 2.6, docker-py must be used. Otherwise, it is recommended to install the docker Python module. Note that both modules should not be installed at the same time.
    Docker API >= 1.20
    Only to be able to logout (state=absent): the docker command line utility

## Role Variables

| Name | Type | Default | Required |
|:----:|:-----------:|:-------:|:-------:|
|amazon_ecr_login|Boolean|false|no|
|docker_username|string|null|yes|
|AWS_ACCESS_KEY_ID|String|null|no|
|AWS_SECRET_ACCESS_KEY|String|null|no|
|AWS_DEFAULT_REGION|String|null|no|

## AWS ECR Login

AWS ECR token is generated by using Ansible's `shell` module and AWS CLI; actual login via the same method.
AWS secrets are assumed to be in the environment; pre-generated or passed directly to the role.

## Dependencies


N/A

## Example Usage

Using the role in a playbook or as a task:

```yaml
  - name: Docker login via docker.login
    include_role:
      name: docker.login
    vars:
      amazon_ecr_login: false
      run_once: true
      docker_username: tilixpull
```