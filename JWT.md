# JWT (JSON Web Token)

- JSON is JavaScript Object Notation structure as key and value pair (Similar to python dictionary)
- JWT is a self-contained way to securely transmit data and information between two parties using JSON object.
- JSON Web Tokens can be trusted because each JWT can be digitally signed, which in return allows the server to know if the JWT has been changed at all.
- JWT should be used when dealing with authorization.
- JWT is a greate way for information to be exchanged between the server and client.

---

# JWT Structure,

## JWT is created of three separate parts, separated by dots `.` includes,

- Headers : (a)
- Payload : (b)
- Signature : (c)

```json
aaaaaaaa.bbbbbbbb.cccccccc
```

## JWT Header

- JWT Header usually consider of two parts,
  - **(alg)** The alogrithm for signing
  - **"typ"** The specific type of token
- JWT header is then encoded using Base64 to create the first part of the JWT (a)

## JWT Payload

- JWT Payload consists of the data.
- The payloads data contains claims, and there are three types of claims.
  - Registered
  - Public
  - Private
- The JWT Payload is then encoded using Base64 to create the second part of the JWT. (b)

## JWT Signature

- JWT Signature is created by using the alogrithm in the header to hash out the encoded header, encoded payload with a secret.
- The secret can be anything, but is saved somewhere on the server that the clent does not have access to.
- The signature is the third and final part of JWT (c).

## JWT Eg.

- JWT Header

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

- JWT Payload

```json
{
  "sub": "1234567890",
  "name": "Abc Xyz",
  "given_name": "Abc",
  "family_name": "Pqr",
  "email": "abc@mail.com",
  "admin": true
}
```

- JWT Signature

```json
HMACSHA256(
    base64UrlEncode(header) + "." +
    base64UrlEncode(payload),
    learnonline
)
```

- JWT

```json
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWUsImlhdCI6MTUxNjIzOTAyMn0.KMUFsIDTnFmyG3nMiGM6H9FNFUROf3wh7SmqJp-QV30
```

---
