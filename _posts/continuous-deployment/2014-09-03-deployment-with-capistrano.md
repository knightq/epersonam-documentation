---
title: Deploy via Capistrano
layout: page
tags:
  - deployment
  - capistrano
categories:
  - continuous-deployment
---
You can deploy any kind of Application with capistrano.
It's most commonly used in the Ruby on Rails community.
For some detailed information about Capistrano please checkout [capistranorb.com](http://capistranorb.com) Please include Capistrano in your project. We don't preinstall capistrano on our build servers.

## Capistrano on Codeship

When your capistrano task is ready and working you just need to add the Capistrano Deployment on Codeship. You just need to specify the task we should run for you. Most of the times this is `deploy`.

Checkout our [Deployment Pipelines]({{ site.baseurl }}{% post_url continuous-deployment/2014-09-03-deployment-pipelines %}) if you want to add multiple Capistrano Deployments.

![Capistrano]({{ site.baseurl }}/images/continuous-deployment/capistrano_deployment_setup.png)

## Capistrano with ScriptDeployment

You don't need to use our Capistrano Integration. If you have a more complex Deployment Setup you can call capistrano directly.

```bash
bundle exec cap deploy
```

## Common Errors

### Capistrano is not installed by default

If you don't have Capistrano in your `Gemfile` you need to install it first. Simply add the following command to a script based deployment which runs before the Capistrano deployment.

```bash
gem install capistrano
```

### Deployment fails because of detached checkout

Because Codeship doesn't do a full clone of the repository to speed up build time, you have to fetch the remaining commits and checkout the branch first.

Either add the following commands to your script based deployment or add a script based deployment before the Capistrano deployment and add the steps there.

```bash
git fetch --unshallow
git checkout "${CI_BRANCH}"
```
