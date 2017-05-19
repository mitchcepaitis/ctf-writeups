# r34n1m4710n

### Challenge
- **Competition:** HackIT CTF 2016
- **Category:** Network
- **Points:** 100
- **File:** [top_secret.pcap](./files/top_secret.pcap)

> Recover the password.

### Solution

This one seemed like it might be a lot of work, sifting through entries in a pcap file.  I thought, just in case, I would see if the flag was just hanging out in plaintext somewhere within the file.  Sure enough, it actually was.

```bash
$ strings top_secret_39af3e3ce5a5d5bc915749267d92ba43.pcap | grep -i h4ck
PASS h4ck1t{i_G07_ur_f1l3s}
```

### Flag

`h4ck1t{i_G07_ur_f1l3s}`