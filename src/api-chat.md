## Chat API

- [chat.postMessage](#post-new-message)
- [chat.remove](#remove-message)
- [chat.unsend](#unsend-message)

### Post new message

> Requires authentication.  
> Requires conversation to exist (see `/conversations.open` API)  
> Requires user to be a member of the conversation.

Posts a new message to the conversation

```text
POST /api/v1/chat.postMessage
```

#### Payload

##### Text message

```json
{
  "conversation_id": "27d04535-e772-46a3-b3c9-47821c33047d",
  "content": { "text": "test" }
}
```

##### Image message

You need to upload the image file separately, using the Media API.  
Given the following response:

```json
[
  {
    "id": "410a80cf-b5dd-4a1a-8e6d-4fd468839334",
    "link": "/api/v1/media/content/410a80cf-b5dd-4a1a-8e6d-4fd468839334",
    "caption": null,
    "file_name": "Screenshot 2023-07-19 at 09.38.16.png"
  }
]
```

The post can be as following:

```json
{
  "conversation_id": "27d04535-e772-46a3-b3c9-47821c33047d",
  "attachments": ["410a80cf-b5dd-4a1a-8e6d-4fd468839334"]
}
```

#### Response

Text message:

```json
{
  "id": "56a3e587-3cbb-4d64-b29d-13f9addbaf61",
  "conversation_id": "27d04535-e772-46a3-b3c9-47821c33047d",
  "created_by": "c3a1ae3c-ea82-448b-9c74-567130ac572a",
  "created_at": 1697985209235,
  "unsent_at": null,
  "edited_at": null,
  "expires_at": null,
  "content": { "text": "test" },
  "attachments": null
}
```

Message with image attachment:

```json
{
  "id": "7575528f-086c-4843-85a6-7c0c4fe37d59",
  "conversation_id": "27d04535-e772-46a3-b3c9-47821c33047d",
  "created_by": "c3a1ae3c-ea82-448b-9c74-567130ac572a",
  "created_at": 1697985623748,
  "unsent_at": null,
  "edited_at": null,
  "expires_at": null,
  "content": null,
  "attachments": [
    {
      "id": "410a80cf-b5dd-4a1a-8e6d-4fd468839334",
      "link": "/api/v1/media/content/410a80cf-b5dd-4a1a-8e6d-4fd468839334",
      "name": "Screenshot 2023-07-19 at 09.38.16.png",
      "mime_type": "image/png"
    }
  ]
}
```

#### Errors

The conversation does not exist:

```json
{
  "ok": false,
  "error": "operation_not_allowed"
}
```

#### Remove Message

> Requires authentication

Deletes a message from the current user feed

```text
POST /api/v1/chat.remove?mid={uuid}
```

Response

```json
{
  "ok": true,
  "id": "56a3e587-3cbb-4d64-b29d-13f9addbaf61"
}
```

### Unsend Message

> Requires authentication.

Marks the message as `Unsent` for everyone.  
Removes message text and attachments.

```text
POST /api/v1/chat.unsend?mid={uuid}
```

Response

```json
{
  "ok": true,
  "id": "7575528f-086c-4843-85a6-7c0c4fe37d59"
}
```
