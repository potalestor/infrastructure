# Infrastructure

## Keycloak

Create creds
```bash
openssl req -x509 -out keycloak.crt -keyout keycloak.key \
  -newkey rsa:4096 -nodes -sha256 \
  -subj '/CN=localhost' -extensions EXT -config <( \
   printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")
```


Request

```bash
make up

curl --location 'http://localhost:8180/realms/realm-test/protocol/openid-connect/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=client-test' \
--data-urlencode 'client_secret=syaYK2PHBIAmuBVDZTkh07qpjxBpbU8r'


curl --location 'https://localhost:8843/realms/realm-test/protocol/openid-connect/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=client-test' \
--data-urlencode 'client_secret=syaYK2PHBIAmuBVDZTkh07qpjxBpbU8r'
```

Response

```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJQc2pxSkdtTmZOdlJqOGw2Y0UzTUx5bTBPa0gwMnJuSkRuZzZRZjZVY0pVIn0.eyJleHAiOjE2ODQ0NDIxODQsImlhdCI6MTY4NDQ0MTg4NCwianRpIjoiZDc2MmMzNzAtNmQwNC00YzE3LWIyYmMtYWRkMjQ1ZDBlYmRkIiwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo4MTgwL3JlYWxtcy9yZWFsbS10ZXN0Iiwic3ViIjoiZGMxZTI5NzAtZDFhYy00ZDYwLTgwMTgtZDI3MzBkMzNiNzZhIiwidHlwIjoiQmVhcmVyIiwiYXpwIjoiY2xpZW50LXRlc3QiLCJzZXNzaW9uX3N0YXRlIjoiM2FmNGY2ZDItOGZmYS00OGE3LTkwNDItMTQyMTA0MjE2MmI0Iiwic2NvcGUiOiJjbGllbnQ6c2NvcGU6dGVzdCIsInNpZCI6IjNhZjRmNmQyLThmZmEtNDhhNy05MDQyLTE0MjEwNDIxNjJiNCIsImNsaWVudEhvc3QiOiIxNzIuMjEuMC4xIiwiY2xpZW50QWRkcmVzcyI6IjE3Mi4yMS4wLjEiLCJjbGllbnRfaWQiOiJjbGllbnQtdGVzdCJ9.aQyDJG2JRZ-8Yk8yVv_mIYX092Dy6vuY3lQiG7Vw8ShKHeCWeDlYfxEuatvfjs8EGfKWjEBMyp3RntlndPagfXM0wxtKJkFh8s3WNvm2qo93DlFN9kSsFB5zjEj5LBZDah8IbCZhY8k6UVwFuTkIGbQ1hfXTxAC-liy94H5rH7IJniNma0ckcQpGJlt-sImgLKA3bUBYYXNJy4T49EtiB3Q0rHd9tTiZvDXp0v2dj3M3Y9j2uV_5k7127nhZgWtJQLjwi9c_dDGTf8-j9GJNQI1G4fgUYoiOYib3dCa5at_lYNJSIhADDXOGvMpF2sIh0410cjV4dcfTCyYSmrlzRQ",
  "expires_in": 300,
  "refresh_expires_in": 1800,
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI2MTFjM2ZlNi0wNWVmLTQyMDUtYWMzYi0wNWI1NDA4NWQwNTIifQ.eyJleHAiOjE2ODQ0NDM2ODQsImlhdCI6MTY4NDQ0MTg4NCwianRpIjoiZWU5YTJkYTgtYWQwZi00NjJlLWI1YWMtMmYxMzcyNzNjZTU3IiwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo4MTgwL3JlYWxtcy9yZWFsbS10ZXN0IiwiYXVkIjoiaHR0cDovL2xvY2FsaG9zdDo4MTgwL3JlYWxtcy9yZWFsbS10ZXN0Iiwic3ViIjoiZGMxZTI5NzAtZDFhYy00ZDYwLTgwMTgtZDI3MzBkMzNiNzZhIiwidHlwIjoiUmVmcmVzaCIsImF6cCI6ImNsaWVudC10ZXN0Iiwic2Vzc2lvbl9zdGF0ZSI6IjNhZjRmNmQyLThmZmEtNDhhNy05MDQyLTE0MjEwNDIxNjJiNCIsInNjb3BlIjoiY2xpZW50OnNjb3BlOnRlc3QiLCJzaWQiOiIzYWY0ZjZkMi04ZmZhLTQ4YTctOTA0Mi0xNDIxMDQyMTYyYjQifQ.BjmLfgvJQuxCn38gV3l-O1hwTEdZnNWvtgbPEnc41go",
  "token_type": "Bearer",
  "not-before-policy": 0,
  "session_state": "3af4f6d2-8ffa-48a7-9042-1421042162b4",
  "scope": "client:scope:test"
}
```