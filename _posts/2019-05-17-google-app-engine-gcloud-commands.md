---
layout: post
title: Basic gcloud Commands for Google App Engine
tags: google-app-engine
---

Let's see basic `gcloud` commands for Google App Engine.

## Install gcloud command on MacOS

```console
$ brew cask install google-cloud-sdk
```

If you're not a MacOS user, please visit [here](https://cloud.google.com/sdk/docs/).

## Local Development

`dev_appserver.py` is useful for local development.

```console
$ dev_appserver.py app.yaml
```

If command not found on MacOS, create a symbolic link.

```console
$ ln -s /usr/local/Caskroom/google-cloud-sdk/latest/google-cloud-sdk/bin/dev_appserver.py /usr/local/bin/dev_appserver.py
```

## Deploy

```console
$ gcloud app deploy
```

This command deploys your application to Google App Engine.

### Deploy Log Sample

```console
$ gcloud app deploy --project {your_project_name}
Services to deploy:

descriptor:      [/your/project/path/app.yaml]
source:          [/your/project/path]
target project:  [your_project_name]
target service:  [default]
target version:  [20190517t173453]
target url:      [https://your_project_name.appspot.com]


Do you want to continue (Y/n)?  Y

Beginning deployment of service [default]...
╔════════════════════════════════════════════════════════════╗
╠═ Uploading 2 files to Google Cloud Storage                ═╣
╚════════════════════════════════════════════════════════════╝
File upload done.
Updating service [default]...done.
Setting traffic split for service [default]...done.
Deployed service [default] to [https://your_project_name.appspot.com]
```

## Browse App

```
$ gcloud app browse
```

This command opens your application url(`https://your_project_name.appspot.com`) on the browser.

## See log

You can watch your application log.

```
$ gcloud app logs tail -s default
```

## Cron deployment

If you want to deploy your cron, run the following command.

```
$ gcloud app deploy cron.yaml
```

## list projects

You can list your own projects on GCP.

```console
$ gcloud projects list
PROJECT_ID   NAME        PROJECT_NUMBER
project-name project     xxxxxxx
project-name project     xxxxxxx
project-name project     xxxxxxx
```

## Specifying Project

You can specify project by adding below option.

```
--project={project}
```
