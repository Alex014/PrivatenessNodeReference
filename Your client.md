# Writing your own client (python)
## Codebase
### Python
Version 3.10
### Libraries
[NaCl](https://pypi.org/project/PyNaCl/)
### NessAuth.py
`def   get_by_auth_id(self, node_full_url: str, user_private_key: str, node_url: str, node_nonce: str, username: str, user_nonce: str):`
Authenticate user by Authentication ID and return data from the node
* node\_full\_url - The full URL of the node you're querying
* user\_private\_key - The private key of the user who is trying to authenticate
* node_url - The URL of the node you're connecting to
* node_nonce - cryptographic salt
* username - The username of the user who is connecting to node
* user_nonce - cryptographic salt

`def   get_by_two_way_encryption(self, node_full_url: str, data: str, node_public_key: str, user_private_key: str, username: str):`
Authenticate user by Two-Way encription and return data from the node
* node\_full\_url - The full URL of the node you're querying
* data - The data you want to send to the node
* node_public_key - The public key of the node you're sending the data to
* user\_private\_key: The private key of the user who is trying to authenticate
* username - The username of the user who is connecting to node

`def   verify_two_way_result(self, node_verify_key: str, result: dict):`
Verify the signature of the data in the result dictionary using the node's verify key
 * node_verify_key - The verify key of the node you're sending the request to
 * result - Data returned by the node

`def   decrypt_two_way_result(self, result: dict, user_private_key: str):`
Decrypt the data in the result dictionary using user's private key
* result - Data returned by the node
* user\_private\_key: The private key of the user who is trying to authenticate

#### Auth ID
Example (taken fron Ness Node Tester):
```python
ness_auth = NessAuth()
user = self.loadUser(username)
node = self.loadNode(node_url)

user_private_key = user['keys']["private"][user['keys']['current']]

result = ness_auth.get_by_auth_id(node_url + "/node/test/auth", user_private_key, node_url, node["nonce"] username, user["nonce"])

if result['result'] == 'error':
  print(' --- TEST 1 Auth ID FAILED --- ')
  print(result['error'])
else:
  print(' *** TEST 1 Auth ID OK !!! *** ')
  print(result['message'])
```
In the example the client tries to authenticate and checks the authentication result
#### Alternate Auth ID
Not implemented yet ...
#### Two way encryption
Example (taken fron Ness Node Tester):
```python
ness_auth = NessAuth()
user = self.loadUser(username)
node = self.loadNode(node_url)

user_private_key = user['keys']["private"][user['keys']['current']]

test_string = 'QWERTY12345678900'

url = node_url + "/node/test/auth"

result = ness_auth.get_by_two_way_encryption(url, test_string, node['public'], user_private_key, username)

if result['result'] == 'error':
	print(" --- TEST 2 Two way encryption FAILED --- ")
	print(result['error'])
else:
	if ness_auth.verify_two_way_result(node['verify'], result):
		print(" *** TEST 2 Two way encryption OK !!! *** ")
		print(ness_auth.decrypt_two_way_result(result, user_private_key))
	else:
		print(" --- TEST 2 Two way encryption FAILED --- ")
		print(" Verifying signature failed ")
```
In the example the client tries to authenticate and checks the authentication result
## File service client example
Not implemented yet ...
