# Cryptoquiz

### Challenge
- **Competition:** Insomnihack Teaser 2017
- **Category:** Crypto / Misc
- **Points:** 50


> Hello, young hacker. Are you ready to fight rogue machines ? Now, you'll have to prove us that you are a genuine cryptographer.
> 
> Running on quizz.teaser.insomnihack.ch:1031


### Solution
After connecting to the challenge server, it sent a simple question:  what year was Claude Shannon born?  I thought, "This is simple", and went to search Google for the birth year of Claude Shannon.  After finding the name, I attempted to send the year back to the server only to find that I had run out of time.  It turned out that two seconds was the allotted time to send a response to the server.  After that time, you are required to reconnect and start over.  After connecting again, birth year already on my clipboard, I was presented with a different name.

Got it.  I need a script to quickly find the presented name, check if I have already looked up the birth year, and return the birth year if known, otherwise alert me so I can look it up and add it to the script.  Surely a more automated solution exists, but this was quick enough.  I ended up finding 52 different birth years.  The script did finally work, and the server returns the flag after many correct responses.

### Script (Python)

```python
import socket
import re


births = {
  "Claude Shannon": "1916",
  "Bart Preneel": "1963",
  "David Naccache": "1967",
  "Ross Anderson": "1956",
  "Claus-Peter Schnorr": "1943",
  "Paul van Oorschot": "1962",
  "Bruce Schneier": "1963",
  "Yvo Desmedt": "1956",
  "Daniel J. Bernstein": "1971",
  "David Chaum": "1955",
  "Mihir Bellare": "1962",
  "Amos Fiat": "1956",
  "Jean-Jacques Quisquater": "1945",
  "Don Coppersmith": "1950",
  "Amit Sahai": "1974",
  "Eli Biham": "1960",
  "Jacques Stern": "1949",
  "Yehuda Lindell": "1971",
  "Moni Naor": "1961",
  "Alex Biryukov": "1969",
  "Ronald Cramer": "1968",
  "Jim Massey": "1934",
  "Dan Boneh": "1969",
  "Shai Halevi": "1966",
  "Victor S. Miller": "1947",
  "Gilles Brassard": "1955",
  "Martin Hellman": "1945",
  "Oded Goldreich": "1957",
  "Scott Vanstone": "1947",
  "Shafi Goldwasser": "1958",
  "Serge Vaudenay": "1968",
  "Ueli Maurer": "1960",
  "Joan Daemen": "1965",
  "Michael O. Rabin": "1931",
  "Paul Kocher": "1973",
  "Whitfield Diffie": "1944",
  "Wang Xiaoyun": "1966",
  "Daniel Bleichenbacher": "1964",
  "Neal Koblitz": "1948",
  "Niels Ferguson": "1965",
  "Kaisa Nyberg": "1948",
  "Horst Feistel": "1915",
  "Moni Naor": "1961",
  "Ralph Merkle": "1952",
  "Rafail Ostrovsky": "1963",
  "Phil Rogaway": "1962",
  "Douglas Stinson": "1956",
  "Adi Shamir": "1952",
  "Tatsuaki Okamoto": "1952",
  "Ron Rivest": "1947",
  "Antoine Joux": "1967",
  "Jacques Patarin": "1965"
}

TCP_IP = 'quizz.teaser.insomnihack.ch'
TCP_PORT = 1031

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

s.connect((TCP_IP, TCP_PORT))
header = s.recv(1024)
print header


while True:
  data = s.recv(1024)
  print data
  if data != '':
    search = re.findall(r'(~~ What is the birth year of )(.*)(\s\?)', data)
    if search:
      name = search[0][1]
      if name and name not in births:
        print "Couldn't find %s." % name
        break
      elif name and name in births:
        s.send(births[name])
        s.send("\n")
        print "Sent %s's birth year: %s" % (name, births[name])
        continue
    else:
	continue
  else:
  	break
  	
s.close()
```


### Flag

`INS{GENUINE_CRYPTOGRAPHER_BUT_NOT_YET_A_PROVEN_SKILLED_ONE}`