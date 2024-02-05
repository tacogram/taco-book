## Users API

- [users.list](#list-users)

### List Users

```text
GET /api/v1/users.list
```

#### Response

```json
[
    {
        "id": "00000000-0000-0000-0000-000000000000",
        "first_name": "Taco",
        "last_name": "Server",
        "email": "admin@taco.app",
        "last_seen": null
    },
    {
        "id": "1986c177-2d48-415d-9c40-169589d6e6cf",
        "first_name": "John",
        "last_name": "Doe",
        "email": "john.doe@taco.app",
        "last_seen": 1697989512021
    }
]
```

#### Errors

```json
{
    "ok": false,
    "error": "Unauthorized"
}
```
