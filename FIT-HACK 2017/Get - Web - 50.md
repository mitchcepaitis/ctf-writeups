# Get

### Challenge
- **Competition:** FIT-HACK 2017
- **Category:** Web
- **Points:** 50
- **File:** [get.pcapng](./files/get.pcapng)

### Solution
This challenge provides a .pcapng file with some traffic.  The name of the challenge was a clue to look at GET requests.  The flag is Base 64 encoded as the `Authorization` header in the GET request for `/icons/ubuntu-logo.png`:

`Authorization: Basic Zml0aGFjazpGSVR7MzMyZHJlZjNhNWc3aH0=`

Base 64 decoding the string `Zml0aGFjazpGSVR7MzMyZHJlZjNhNWc3aH0` reveals the flag.

### Flag

`FIT{332dref3a5g7h}`