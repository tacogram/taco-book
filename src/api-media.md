## Media API

- `POST /api/v1/media/content`
- `GET /api/v1/media/content/{uid}`
- `POST /api/v1/media/avatars`
- `GET /api/v1/media/avatars/{uid}`

### Upload Media

> Requires authentication

Provides support for multipart form data

```text
POST /api/v1/media/content
```

Returns a list of Media Blocks

```json
[
  {
    "id": "uuid",
    "link": "string",
    "file_name": "(optional) string",
    "caption": "(optional) string"
  }
]
```

### Get Uploaded Media

> Requires authentication

Provides access to the user media

```text
GET /api/v1/media/content/{uuid}
```

Returns file content stream

### Set Avatar Image

> Requires authentication

Uploads current user avatar image

```text
POST /api/v1/media/avatars
```

### Get Avatar Image

> Requires authentication

Provides access to user avatar images

```text
/api/v1/media/avatars/{uid}
```
