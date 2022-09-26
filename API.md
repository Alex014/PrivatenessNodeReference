# Service Node API

## How it works
The client communicates with Service Node by 3 ways:
### Plain
The most simple way of communication: Request -> Response, no encryption used.
### Auth ID
Authentication through auth-id, which is a prt of URL.

auth-id is formed in the folowing way:
```
message = node.url + "-" + node.nonce + "-" + username + '-' + user.nonce
auth-id = sign(user.private_key, message)
```
Signature is base32 encoded, but all keys are base64 encoded
### Alternative ID
Similar to Auth ID, but used in file download.
```
message = node.url + "-" + node.nonce + "-" + username + '-' + user.nonce + '-alternative'
auth-id = sign(user.private_key, message)
```
Signature is base32 encoded, but all keys are base64 encoded
### Shadowname
Used to increase security stored in service/server side, auto-generated on registration.
### Two-Way encryption
The data being sent to service/server side is encrypted and then signed.
```
encrypted_data = encrypt(data, node.public_key)
signature = sign(user.private_key, encrypted_data)
```
Signature is base32 encoded, but all keys are base64 encoded, encrypted data also base64 encoded
#### Return data (JSON)
* error
```
{"result": "error", "error": "Error description text"}
```
* info
```
{"result": "info", "info": "Info text"}
```
* data
```
{"result": "data", "data": "Data"}
```
* message
```
{"result": "message", "message": "Message text"}
```
* encrypted
```
{"result": "encrypted", "data": "Base64 encrypted data", "sig": "base32 signature"}
```
## Node service

### API

#### Plain
* nodes

* services

* pub

* verify

* slots

#### Two-Way
* join

* joined

* balance

* userinfo

* withdraw

### Tests

## PRNG service

### Auth ID
* seed

* seedb

* numbers

* numbersb

* i256

* h256


### Tests

## Files service

### API

#### Auth ID
 * download

 * upload


#### Alternative ID
 * pub

#### Two-Way
* quota

* list

* fileinfo

* touch

* remove

### Tests
