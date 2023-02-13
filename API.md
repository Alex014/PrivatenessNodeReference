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
```
$shadowname = md5(username-node.url-nonce-user.nonce: time())
```
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
Always returned unencrypted
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
* encrypted (Two-Way encryption)
```
{"result": "encrypted", "data": "Base64 encrypted data", "sig": "base32 signature"}
```
## Node service

### API

#### Plain
* nodes

Return full list of nodes from blockchain

URL: `http://node-url.net/node/nodes`
* services

Returns list of awailable services

URL: `http://node-url.net/node/services`
* pub

Returns public key of current service node

URL: `http://node-url.net/node/pub`
* verify

Returns verify key of current service node

URL: `http://node-url.net/node/verify`
* slots

Returns amount of open slots (awailable places for new users)

URL: `http://node-url.net/node/slots`

#### Two-Way
* join

User registration

URL: `http://node-url.net/node/join`

In (POST): 

`username`, `data` - any random data, `sig` - signature of data

Return data (JSON):

`address` - generated user address in Privateness blockchain

`shadowname` - newly generated shadowname of user

or ERROR

* joined

Is user registered (joined)

URL: `http://node-url.net/node/joined`

In (POST):

`username`, `data` - any random data, `sig` - signature of data

Return data (JSON):

`joined` - is user joined

`address` - generated user address in Privateness blockchain

`shadowname` - newly generated shadowname of user

* balance

Return joined user balance

URL: `http://node-url.net/node/balance`

In (POST):

`username` - shadowname, `data` - any random data, `sig` - signature of data

Return data (JSON):

`balance` - balance in *NESS* and *NCH*

* userinfo

Return joined user info

URL: `http://node-url.net/node/userinfo`

In (POST):

`username` - shadowname, `data` - any random data, `sig` - signature of data

Return data (JSON):

`userinfo` - 

*balance* - balance in *NESS* and *NCH*,

*joined* - is user joined, 

*is_active* - is user active (has positive balance)

* withdraw

Withdraw funds

URL: `http://node-url.net/node/withdraw`

In (POST):

`shadowname`, `data` - encrypted JSON:

*coins* - amound of NESS to withdraw

*hours* - amound of NCH to withdraw

*to_addr* - external Privateness address

, `sig` - signature of data

Return: success - TEXT

## PRNG service

### Auth ID
* seed
URL: `http://node-url.net/prng/seed/username/auth-id`
Return (JSON):
`seed` - randomly generated string
* seedb
URL: `http://node-url.net/prng/seedb/username/auth-id`
Return (JSON):
`seedb` - randomly generated string (big)
* numbers
URL: `http://node-url.net/prng/numbers/username/auth-id`
Return (JSON):
`numbers` - [float, ...]
Randomly generated array of float numbers
* numbersb
URL: `http://node-url.net/prng/numbersb/username/auth-id`
Return (JSON):
`numbersb` - [float, ...]
Randomly generated array of float numbers (bigger ammount)
* i256
URL: `http://node-url.net/prng/i256/username/auth-id`
Return (JSON):
`numbersb` - [i256, ...]
Randomly generated array of integer (i256) numbers
* h256
URL: `http://node-url.net/prng/h256/username/auth-id`
Return (JSON):
`numbersb` - [h256, ...]
Randomly generated array of hex (h256) numbers

## Files service

### File ID
Service/Server generated file ID

```$file_id = sha1($filename + salt)```

### API

#### Auth ID
 * download

Internal dawnload link for selected file

URL: `http://node-url.net/files/download/$file_id/$shadowname/$auth-id`

Return: File download with resume support via HTTP headers

 * append

Upload a part of file and append this part to existing (olready created by *touch*) file.

URL: `http://node-url.net/files/append/$file_id/$shadowname/$auth-id`

INPUT: file body inside HTTP request

Return data (JSON):

`size`: file size on server

or ERROR

#### Alternative ID
 * pub

External dawnload link for selected file

URL: `http://node-url.net/files/pub/$file_id-$shadowname-$alternative-id`

Return: File download with resume support via HTTP headers

#### Two-Way
* quota

Used, Free and total user's quota in bytes

In (POST):

`username` - shadowname of user, `data` - any random data, `sig` - signature of data

URL: `http://node-url.net/files/quota`

Return (JSON):

`total`: total space awailable for user in bytes

`used`: used space in bytes

`free`: free left space in bytes

* list

List of all users file

In (POST):

`username` - shadowname of user, `data` - any random data, `sig` - signature of data

URL: `http://node-url.net/files/list`

Return (JSON):

[ {

`filename`: filename

`size`: file size

`id`: file ID

}, ... ]

* fileinfo

In (POST):

`username` - shadowname of user, `file_id` - file ID,  `data` - any random data, `sig` - signature of data

Information about file

URL: `http://node-url.net/files/fileinfo`

Return (JSON):

`filename`: filename

`size`: file size

`id`: file ID

or ERROR if file does not exist

* touch

In (POST):

`username` - shadowname of user, `filename` - encrypted filename,  `data` - any random data, `sig` - signature of data

Create file

URL: `http://node-url.net/files/touch`

Return data (JSON):

`size`: 0

`id`: File ID

if file was created

or ERROR if file not created

* remove

Delete file

URL: `http://node-url.net/files/remove`

Return (TEXT): OK

or ERROR if file wa not removed
