# JWT Claim Fields and Header Fields

- [List of abbreviations that can be found within a token](https://en.wikipedia.org/wiki/JSON_Web_Token)
- The date is in epoch and can be converted [here](https://www.epochconverter.com/)

## Standard claim fields

The internet drafts define the following standard fields ("claims") that can be used inside a JWT claim set.

| Code | Name         | Description |
|------|--------------|-------------|
| iss  | Issuer       | Identifies the principal that issued the JWT. |
| sub  | Subject      | Identifies the subject of the JWT. |
| aud  | Audience     | Identifies the recipients that the JWT is intended for. Each principal intended to process the JWT must identify itself with a value in the audience claim. If the principal processing the claim does not identify itself with a value in the aud claim when this claim is present, then the JWT must be rejected. |
| exp  | Expiration Time | Identifies the expiration time on and after which the JWT must not be accepted for processing. The value must be a NumericDate (either an integer or decimal), representing seconds past 1970-01-01 00:00:00Z. |
| nbf  | Not Before   | Identifies the time on which the JWT will start to be accepted for processing. The value must be a NumericDate. |
| iat  | Issued at    | Identifies the time at which the JWT was issued. The value must be a NumericDate. |
| jti  | JWT ID       | Case-sensitive unique identifier of the token even among different issuers. |

## Commonly-used header fields

The following fields are commonly used in the header of a JWT.

| Code | Name         | Description |
|------|--------------|-------------|
| typ  | Token type   | If present, it must be set to a registered IANA Media Type. |
| cty  | Content type | If nested signing or encryption is employed, it is recommended to set this to JWT; otherwise, omit this field. |
| alg  | Message authentication code algorithm | The issuer can freely set an algorithm to verify the signature on the token. However, some supported algorithms are insecure. |
| kid  | Key ID       | A hint indicating which key the client used to generate the token signature. The server will match this value to a key on file in order to verify that the signature is valid and the token is authentic. |
| x5c  | x.509 Certificate Chain | A certificate chain in RFC4945 format corresponding to the private key used to generate the token signature. The server will use this information to verify that the signature is valid and the token is authentic. |
| x5u  | x.509 Certificate Chain URL | A URL where the server can retrieve a certificate chain corresponding to the private key used to generate the token signature. The server will retrieve and use this information to verify that the signature is authentic. |
| crit | Critical     | A list of headers that must be understood by the server in order to accept the token as valid. |