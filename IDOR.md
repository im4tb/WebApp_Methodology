IDOR API TESTING
**API1:2019 Broken Object Level Authorization**

- Add parameter to the endpoint

```html
GET /api_v1/messages --> 401
vs 
GET /api_v1/messages?user_id=victim_uuid --> 200
```

**Note**: Useful tool to bruteforce common IDOR URL parameter names[Arjun](https://github.com/s0md3v/Arjun).
