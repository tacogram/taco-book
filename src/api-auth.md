## Auth API

- [Register](#register)
- [Login](#login)
- [Logout](#logout)

### Register

```text
POST /api/v1/auth/register
```

Payload

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john.doe@taco.app",
  "password": "password"
}
```

#### Register Response

```json
{
  "ok": true
}
```

#### Register Errors

Email conflict

```json
{
  "ok": false,
  "error": "User with that email already exists"
}
```

### Login

```text
POST /api/v1/auth/login
```

```json
{
  "email": "admin@admin.com",
  "password": "password123"
}
```

#### Login Response

```json
{
  "ok": true,
  "access_token": "<jwt-token>",
  "refresh_token": "<jwt-token>"
}
```

#### Login Errors

User is not registered

```json
{
  "ok": false,
  "error": "Not found"
}
```

Invalid credentials

```json
{
  "ok": false,
  "error": "Invalid email or password"
}
```

### Token

Header (see <https://jwt.io/>)

```json
{
  "typ": "JWT",
  "alg": "RS256"
}
```

Payload

```json
{
  "iss": "taco",
  "sub": "c3a1ae3c-ea82-448b-9c74-567130ac572a",
  "iat": 1698604128,
  "exp": 1698605028,
  "nbf": 1698604128,
  "context": {
    "email": "denys.vuika@taco.app",
    "roles": [
      "user"
    ],
    "first_name": "Denys",
    "last_name": "Vuika"
  }
}
```

### Logout

> Requires authentication

Logs user out of the system

```text
GET /api/v1/auth/logout
```

#### Logout Response

```json
{
  "ok": true
}
```

#### Logout Errors

User is not logged in

```json
{
  "ok": false,
  "error": "Unauthorized"
}
```
