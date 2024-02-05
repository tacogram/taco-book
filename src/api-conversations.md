## Conversations API

- [conversations.list](#list-conversations)
- [conversation.info](#conversation-info)
- [conversations.replies](#list-conversation-replies)
- [conversations.members](#list-conversation-members)
- [conversations.archive](#archive-conversation)
- [conversations.unarchive](#unarchive-conversation)
- [conversations.delete](#delete-conversation)
- [conversations.match](#match-existing-conversation)
- [conversations.open](#open-new-conversation)

### List Conversations

> Requires authentication

Lists all conversations the current user is member of.

```text
GET /api/v1/conversations.list
GET /api/v1/conversations.list?limit={number}
```

#### Response

```json
[
  {
    "id": "49d559ac-497c-42cf-a06d-3a4e7328b296",
    "created_by": "cf7195c7-9f6a-408e-9325-f8f15bf6edeb",
    "conversation_type": "direct",
    "last_msg_text": "You sent a photo • 2:04 PM",
    "last_msg_uid": "c3a1ae3c-ea82-448b-9c74-567130ac572a",
    "archived": false,
    "joined_at": 1697914809267,
    "participants": [
      {
        "id": "cf7195c7-9f6a-408e-9325-f8f15bf6edeb",
        "first_name": "Jordyn",
        "last_name": "Frank",
        "email": "Jordyn.Frank@taco.app",
        "last_seen": null
      },
      {
        "id": "c3a1ae3c-ea82-448b-9c74-567130ac572a",
        "first_name": "Denys",
        "last_name": "Vuika",
        "email": "denys.vuika@taco.app",
        "last_seen": null
      }
    ]
  }
]
```

### Conversation Info

> Requires authentication.  
> Displays only conversations current user is a member of

Gets information on a single conversation thread

```text
GET /api/v1/conversations.info?cid={uuid}
```

#### Response

```json
{
  "ok": true,
  "conversation": {
    "id": "49d559ac-497c-42cf-a06d-3a4e7328b296",
    "created_by": "cf7195c7-9f6a-408e-9325-f8f15bf6edeb",
    "conversation_type": "direct",
    "last_msg_text": "You sent a photo • 2:04 PM",
    "last_msg_uid": "c3a1ae3c-ea82-448b-9c74-567130ac572a",
    "archived": false,
    "joined_at": 1697914809267,
    "participants": [
      {
        "id": "c3a1ae3c-ea82-448b-9c74-567130ac572a",
        "first_name": "Denys",
        "last_name": "Vuika",
        "email": "denys.vuika@taco.app",
        "last_seen": null
      },
      {
        "id": "cf7195c7-9f6a-408e-9325-f8f15bf6edeb",
        "first_name": "Jordyn",
        "last_name": "Frank",
        "email": "Jordyn.Frank@taco.app",
        "last_seen": null
      }
    ]
  }
}
```

Or empty response:

```json
{
  "ok": true,
  "conversation": null
}
```

#### Errors

```json
{
  "ok": false,
  "error": "<message>"
}
```

### List Conversation Replies

> Needs authentication, user must be a conversation participant

```text
GET /api/v1/conversations.replies?cid={uuid}
GET /api/v1/conversations.replies?cid={uuid}&ts_from={timestamp}&ts_to={timestamp}&limit={number}
```

#### Result

```json
[
  {
    "id": "b90d8dd0-3779-427a-afc5-3fcd672015f9",
    "conversation_id": "49d559ac-497c-42cf-a06d-3a4e7328b296",
    "created_by": "cf7195c7-9f6a-408e-9325-f8f15bf6edeb",
    "created_at": "2023-10-07T19:56:11.552980Z",
    "unsent_at": null,
    "edited_at": null,
    "expires_at": null,
    "content": {
      "text": {
        "body": "hello"
      }
    },
    "attachments": null
  },
  {
    "id": "5cf7a1c2-410b-4637-a677-c6cc28ca58b8",
    "conversation_id": "49d559ac-497c-42cf-a06d-3a4e7328b296",
    "created_by": "cf7195c7-9f6a-408e-9325-f8f15bf6edeb",
    "created_at": "2023-10-07T19:57:11.552980Z",
    "unsent_at": null,
    "edited_at": null,
    "expires_at": null,
    "content": null,
    "attachments": [
      {
        "id": "18109dea-17cb-42bf-8196-f7d41e3aa593",
        "link": "/api/v1/media/content/18109dea-17cb-42bf-8196-f7d41e3aa593",
        "name": "file-1.jpg",
        "mime_type": "image/jpg"
      }
    ]
  }
]
```

### List Conversation Members

> Requires authentication

Requires user to be part of the conversation.

```text
GET /api/v1/conversations.members?cid={uuid}
GET /api/v1/conversations.members?cid={uuid}&limit={number}
```

#### Response

```json
[
  {
    "id": "e2b6bf46-3854-489e-b050-607520222a5a",
    "first_name": "Ephraim",
    "last_name": "Gonzalez",
    "email": "Ephraim.Gonzalez@taco.app",
    "last_seen": null
  },
  {
    "id": "c3a1ae3c-ea82-448b-9c74-567130ac572a",
    "first_name": "Denys",
    "last_name": "Vuika",
    "email": "denys.vuika@taco.app",
    "last_seen": null
  }
]
```

### Archive Conversation

```text
`POST /api/v1/conversations.archive?cid={uuid}`
```

#### Response

```json
{ "ok": true }
```

#### Errors

Authentication error:

```json
{
  "ok": false,
  "error": "Unauthorized"
}
```

Error parsing query parameters:

```json
{
  "ok": false,
  "error": "Query deserialize error: UUID parsing failed: invalid group count: expected 5, found 6"
}
```

### Unarchive Conversation

```text
POST /api/v1/conversations.unarchive?cid={uuid}
```

Response:

```json
{ "ok": true }
```

### Delete Conversation

> Requires authentication.  
> Requires user to be a member of the conversation.

```text
POST /api/v1/conversations.delete?cid={uuid}
```

### Match existing conversation

> Requires authentication.  
> Requires user to be part of the conversation.

Matches existing conversation by the list of members.
The conversation must have exact list of participants, the order of user IDs is optional.

```text
POST /api/v1/conversations.match

{
    "users": [
      "e29bbd89-0a2e-4b9b-adfe-6511f3b8ebdc",
      "c3a1ae3c-ea82-448b-9c74-567130ac572a"
    ]
}
```

#### Response

Existing conversation (can be opened)

```json
{
  "ok": true,
  "conversation": {
    "id": "1962c32e-5155-4468-b01d-5f93315e7fd8",
    "created_by": "e29bbd89-0a2e-4b9b-adfe-6511f3b8ebdc",
    "conversation_type": "direct",
    "last_msg_text": "test",
    "last_msg_uid": "c3a1ae3c-ea82-448b-9c74-567130ac572a",
    "archived": false,
    "joined_at": 1697914809267,
    "participants": [
      {
        "id": "c3a1ae3c-ea82-448b-9c74-567130ac572a",
        "first_name": "Denys",
        "last_name": "Vuika",
        "email": "denys.vuika@taco.app",
        "last_seen": null
      },
      {
        "id": "e29bbd89-0a2e-4b9b-adfe-6511f3b8ebdc",
        "first_name": "Imaad",
        "last_name": "Casey",
        "email": "Imaad.Casey@taco.app",
        "last_seen": null
      }
    ]
  }
}
```

Missing conversation (can be created)

```json
{
  "ok": true,
  "cid": null
}
```

#### Errors

Authentication error:

```json
{
  "ok": false,
  "error": "Unauthorized"
}
```

Users is not allowed to see the conversation they are not part of:

```json
{
  "ok": false,
  "error": "operation_not_allowed"
}
```

Incorrect payload format:

```json
{
  "ok": false,
  "error": "Json deserialize error: invalid type: integer `1`, expected a UUID string at line 2 column 15"
}
```

### Open New Conversation

> Requires authentication.

Creates a new conversation by the list of members.

The originator is automatically added to the conversation as a participant.

```text
POST /api/v1/conversations.open

{
    "users": [
      "e29bbd89-0a2e-4b9b-adfe-6511f3b8ebdc",
      "c3a1ae3c-ea82-448b-9c74-567130ac572a"
    ]
}
```

#### Conversation Types

The resulting type of the conversation depends on the amount of participants:

- 0 - not allowed
- 1 - public channel
- 2 - direct conversation
- 3/+ - group conversation

#### Response

Existing conversation (can be opened)

```json
{
  "ok": true,
  "conversation": {
    "id": "1962c32e-5155-4468-b01d-5f93315e7fd8",
    "created_by": "e29bbd89-0a2e-4b9b-adfe-6511f3b8ebdc",
    "conversation_type": "direct",
    "last_msg_text": "test",
    "last_msg_uid": "c3a1ae3c-ea82-448b-9c74-567130ac572a",
    "archived": false,
    "joined_at": 1697914809267,
    "participants": [
      {
        "id": "c3a1ae3c-ea82-448b-9c74-567130ac572a",
        "first_name": "Denys",
        "last_name": "Vuika",
        "email": "denys.vuika@taco.app",
        "last_seen": null
      },
      {
        "id": "e29bbd89-0a2e-4b9b-adfe-6511f3b8ebdc",
        "first_name": "Imaad",
        "last_name": "Casey",
        "email": "Imaad.Casey@taco.app",
        "last_seen": null
      }
    ]
  }
}
```
