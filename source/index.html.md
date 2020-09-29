---
title: Canopeo API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Replacement for the Canopeo backend, written in Node.JS.

# Status

```shell
curl https://canopeoapp.com/canopeo/api/v1/status
```
> Response

```shell
ONLINE
```

This route fetches the online status of the API.

# Authentication

## Obtaining a Token

```shell
curl --header "Content-Type: application/json" --request POST \
--data '{"username":"your_username","password":"your_password"}' \
https://canopeoapp.com/canopeo/api/v1/api-token-auth
```

> Response:

```json
{
  "token":  "v13pGiSaKUwWh1RWaWy8G8Nzbafgv_ZrQ"
}
```

To access the Canopeo API, you will need an **access token**. To obtain one, make a cURL like the following:

### HTTP Request

`POST /api-token-auth`

## Resetting Password:

```shell
curl --header "Content-Type: application/json" --request POST --data '{"email":"your_email"}' \
https://canopeoapp.com/canopeo/api/v1/reset
```

> The result is a Password Request Email being sent to you. After the email containing the token arrives, do the following:

```shell
curl https://canopeoapp.com/canopeo/api/v1/rest/your_token
```

> Response:

```html
The password for <username> has been reset. Your new password is:

<password>

Once you log in using this password, you may update it to something else.
```

This route requests a password reset token. Email must be added.

### HTTP Request:

`POST /reset` OR `POST /reset/1/set_password`

### THEN

`GET /reset/<token>`

# User

## Getting Users

```shell
curl --header "Authorization: Bearer your_access_token" https://canopeoapp.com/canopeo/api/v1/users
```

> Response:

```json
[
  {
    "id":00000,
    "username":"name",
    "email":"name@example.com",
    "first_name":"first_name",
    "last_name":"last_name",
    "time_joined":"2020-05-26T21:31:03.000Z",
    "last_login":"2020-09-24T17:16:06.000Z",
    "is_active":true,
    "is_superuser":0,
    "is_staff":false,
    "extra_security":true,
    "created_at":"2020-05-26T21:31:03.000Z",
    "updated_at":"2020-09-24T17:16:06.000Z"
  }
]

```

This route fetches user information. If you are a superuser, it returns all users in the system.

### HTTP Request:

`GET /users`

## Updating Users

```shell
curl --header "Authorization: Bearer your_access_token" --request PUT \
--data '{"first_name": "fistName", "last_name": "lastName", "email": "email@example.com"}' \
https://canopeoapp.com/canopeo/api/v1/users/<id>

```

> Response

```json
[
  {
    "id":00000,
    "username":"name",
    "email":"name@example.com",
    "first_name":"first_name",
    "last_name":"last_name",
    "time_joined":"2020-05-26T21:31:03.000Z",
    "last_login":"2020-09-24T17:16:06.000Z",
    "is_active":true,
    "is_superuser":0,
    "is_staff":false,
    "extra_security":true,
    "created_at":"2020-05-26T21:31:03.000Z",
    "updated_at":"2020-09-24T17:16:06.000Z"
  }
]

```

This route updates a user's information. Must be authenticated.

### HTTP Request: 

`PUT /users/<id>`

# Fields

## Fetching Fields

```shell
curl "Authorization: Bearer your_access_token" https://canopeoapp.com/canopeo/api/v1/fields
```

> Response                                                                                                                                                                                                                                   

```json
[
  {
    "id":"id",                                                          "name":"field_name",
    "user_id":"user_id",
    "created_at":"createdAt",
    "updated_at":"updatedAt",
  }
]
```

This route fetches a user's fields. Must be authenticated.

### HTTP Request:

`GET /fields`

# Folders

## Fetching Folders

```shell
curl "Authorization: Bearer your_access_token" https://canopeoapp.com/canopeo/api/v1/folders
```

> Response

```json
[
  {
    "id":"id"
    "name":"folder_name"
    "user_id":"user_id"
    "created_at":"createdAt"
    "updated_at":"updatedAt"
  }
]
```

This route fetches a user's folders. Must be authenticated.

### HTTP Request:

`GET /folders`

# Canopeo Data

## Fetching Canopeo Data

> Canopeo Data Object:

```json
[
  {
    "id":00000,
    "data_id":00000,
    "owner_id":00000,
    "owner":"firstName",
    "folder_id":00000,
    "project_folder":,
    "field_id":00000,
    "field_name":"fieldName",
    "date_time":"date",
    "planting_date":"plantDate",
    "canopy_cover":0,
    "adjustments":0,
    "latitude":0,
    "longitude":0,
    "vegetation_type":"Wheat",
    "vegetation_height":0,
    "variety":"Yellow",
    "tillage":0,
    "notes":null,
    "device":"iOS",
    "original_image":"image.jpg",
    "processed_image":"image_processed.jpg", 
    "thumbnail_image":"image_thumb.jpg",
    "video":null,
    "video_rotation":null,
    "created_at":"date",
    "updated_at":"date",
  }
]
```

This route fetches Canopeo Data for a user. Must be Authenticated.

### HTTP Request:

`GET /canopeo/<id>`

## Uploading Canopeo Data

This route uploads Canopeo Data to the database for a user. Must be Authenticated.

### HTTP Request:

`POST /canopeo/<id>`

## Deleting Canopeo Data

This route deletes Canopeo Data for user. Must be Authenticated.

### HTTP Request:

`DELETE /canopeo/data/<id>`

# Export

## Exporting Canopeo Data

These routes export Canopeo Data for a user. Must be Authenticated.

### HTTP Request:

`GET /export` **OR** `GET /canopeo/0/download_user_data`

# Statistics

## Server Statistics

```json
[
  {
    date_time: "2020-07-25T06:00:01.000Z"
    free_size_gb: 523485011968
    number_pictures: 203558
    number_users: 21644
    number_videos: 1248
    usage_percent: 45.33241204818938
    used_size_gb: 532330512384
  }
]
```

This route fetches current server statistics. Must be Authenticated and Superuser.

### HTTP Request: 

`GET /stats`

## Total Server Statistics

```json
[
  {
    androidNum: 67906,
    dateTime: "2020-07-25T06:00:01.000Z",
    id: 189728230,
    iosNum: 113990,
    sizeAndroid: 65833870456,
    sizeIos: 181272092181,
    sizePictures: 247105962637,
    sizeVideos: 14121393012,
  }
]
```

`GET /total_server_stats`

This route fetches the total server statistics. Must be Authenticated and Superuser. The Full Return object is omitted on account of being 8000+ rows.
