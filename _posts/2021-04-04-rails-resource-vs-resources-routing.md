---
layout: post
title: Rails resources vs resource Routing
tags: rails
---

## `resources` routing

### Routing definition

```rb
resources :photos
```

### Routing result

| HTTP Verb | Path             | Controller#Action | Used for                                     |
| --------- | ---------------- | ----------------- | -------------------------------------------- |
| GET       | `/photos`          | `photos#index`      | display a list of all photos                 |
| GET       | `/photos/new`      | `photos#new`        | return an HTML form for creating a new photo |
| POST      | `/photos`          | `photos#create`     | create a new photo                           |
| GET       | `/photos/:id`      | `photos#show`       | display a specific photo                     |
| GET       | `/photos/:id/edit` | `photos#edit`       | return an HTML form for editing a photo      |
| PATCH/PUT | `/photos/:id`      | `photos#update`     | update a specific photo                      |
| DELETE    | `/photos/:id`      | `photos#destroy`    | delete a specific photo                      |

## `resource` routing

### Routing definition

```rb
resource :geocoder
```

### Routing result

| HTTP Verb | Path           | Controller#Action | Used for                                      |
| --------- | -------------- | ----------------- | --------------------------------------------- |
| GET       | `/geocoder/new`  | `geocoders#new`     | return an HTML form for creating the geocoder |
| POST      | `/geocoder`      | `geocoders#create`  | create the new geocoder                       |
| GET       | `/geocoder`      | `geocoders#show`    | display the one and only geocoder resource    |
| GET       | `/geocoder/edit` | `geocoders#edit`    | return an HTML form for editing the geocoder  |
| PATCH/PUT | `/geocoder`      | `geocoders#update`  | update the one and only geocoder resource     |
| DELETE    | `/geocoder`      | `geocoders#destroy` | delete the geocoder resource                  |
