# Math bot

### Challenge
- **Competition:** Alex CTF 2017
- **Category:** SC
- **Points:** 50

> It is well known that computers can do tedious math faster than human.
> 
> nc 195.154.53.62 1337
> Update
> we got another mirror here
> 
> nc 195.154.53.62 7331


### Solution

This challenge required doing simple mathematical operations on rather large integers, about 250 times in a row.  A quick Python script completed this challenge.  My solution script could have been more straightforward, but it worked.

### Script (Python)

```python
import re
import socket
import sys

# CTF Challenge Connection
TCP_IP = '195.154.53.62'
TCP_PORT = 7331

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

try:
  s.connect((TCP_IP, TCP_PORT))
  print("[+] Successfully Connected")
except:
  print("[-] Could Not Connect")
  sys.exit()


def math_operation(data):
  numbers = re.findall(r'(\d+)\s([+\-%/*])\s(\d+)\s', data)[0]
  number1 = int(numbers[0])
  operator = numbers[1]
  number2 = int(numbers[2])
  if operator == "+":
    return (number1 + number2)
  elif operator == "-":
    return (number1 - number2)
  elif operator == "%":
    return (number1 % number2)
  elif operator == "/":
    return (number1 / number2)
  elif operator == "*":
    return (number1 * number2)
  else:
    print("Bad operator: %s" % operator)

while True:
  data = s.recv(1024)
  check_data = re.findall(r'Question\s\s\d+', data)
  if check_data:
    sys.stdout.write(check_data[0] + "\r")
    sys.stdout.flush()
    result = math_operation(data)
    s.send(str(result) + "\n")
  else:
    print data
    break

s.close()
```


### Flag

`ALEXCTF{1_4M_l33t_b0t}`