# Testing
## Running tests
Change your directory to *NessNodeTester*
### Authentication test
Test user authentication

Run: `python test-auth.py <username> <node URL>`
### User test
Request information about existing user

* Address (is no address exists than it will be created)
* Current balance (Coins and Hours, fee)
* Is user active (has enough balance to use node)

Run: `python test-user.py <username> <node URL>`
### Withdraw test
Withdraw coins and hours from existing user to external address

Usage: `python test-withdraw.py <node URL> <username> <address> <coins> <hours>`

```
    <node URL> - node URL
    <username> - Your username
    <address> - External address
    <coins> - Ammount of coins to withdraw
    <hours> - Ammount of hours to withdraw
```
### PRNG service test
Test PRNG service

Usage: `python test-user.py <username> <node URL>`
```
    <node URL> - node URL
    <username> - Your username
```
### Files service test
Test Files service

Usage:
```
Test Files Service
python test-auth.py <username> <node URL> quota --- show users quota (free,used,total)
python test-auth.py <username> <node URL> list --- users files list
python test-auth.py <username> <node URL> upload <filename> --- upload filename to node (with resume)
python test-auth.py <username> <node URL> fileinfo <file_id> --- fileinfo on uploaded file (includes links for download (dl) and public link (pub))
python test-auth.py <username> <node URL> download <file_id> --- download uploaded file (with resume)
```
```
<node URL> - node URL
<username> - Your username
<file_id> - Hash of file name (returned by fileinfo or list commands)
```
