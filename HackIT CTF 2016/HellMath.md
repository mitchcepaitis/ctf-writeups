# HellMath

### Challenge
- **Competition:** HackIT CTF 2016
- **Category:** PPC
- **Points:** 100

> Somebody thinks that you are able to calculate well. Is it true? Pass this task, prove the abilities and maybe we will recommend you to one of the most secret missions in this war.
> nc ctf.com.ua 9988


### Solution

Without a file or more information in the challenge text, the first thing to do was to connect to the server and see what's going on with it.  Upon connecting, the following text is displayed:

```bash
Hello, stranger!

In this task you must solve 100 math questions.
Every task prints value C, where

C = A ^ B,

and you need to return A and B.

Simple, isn't it?
```

Yeah, ok, I can do some math.  Let's see the first value of __C__.

```none
C=1513869083094466114979757219487401502755877733584693998931426104950382732449165255546657643540045011107023697308789187932421055030242698194479699517866528945143811577483859758175950480086710512845455469667762612406539399788035105878454471752964067480299955243042074461323059556643549391036129905323952836948020823216031501568259702378106549434888527812176814138076477912773272021706702630167170126604043159279339645346582972353359887870895955097545845610320548828003385406967521595067297655077375781414953670637252752844134602404475947512037039814121632802652467302317142798493042790158708567641944339738244389566366269488076354068851649598495063743858903305437617683494767145966842503496406584559350146677989797739619879934193906566629858871440774175775526192044628747476366172073365548165634633612286078890125989643160236371042795872215947463361412477298925408712688297880436632410029374583828174046930818195351421629521642082729279745692427512313396170521971686427352054037585516224401931854897817786972105647172900709828692119628785056172537992674058425998909339012433304977606566637405675487587925144298174314972269683576341205042263267520295356333517069094558506645647274966791377832607071399503813572401370229216313758864920341060282227879198170307190614422756545499176869028506217296460901927117917555249104186070118003942219607053932287405516737940158397342726807059784087741160674241366050481549307367825184366159477678208878201382690748508315501988713050573436811099440529363856516886531846602976342374719718595977661349255955874840716614659380607546950839537789431583751998193170277757597392442732320114993165991547984621624347697445326181451243498818615270383242360977102308901308608874341722225143993505915737885960190142864448507820233208993658043337317218550675150498954185493598516641342541247996703988080039259368017296977423087160944672270285892114643337847310217451835546069725953448927300335187555759430494031440853883918790401517978523075897925001384142809549777608458025842154192116139825865876399953449973060441249367881449161474472809989105709144691036243223072621678420038587441491510976519226861402437043074480785979095475333023368579280999652238129529190056319000981792382320587350293339956456003191714702832337215637167292495098885397525690432004444697482573243914384872617156579327717750554115261305214803281733506193770386005109922814246302016996356216783585519393340640819878255813729914018167445085563557876894249296616761913261231702016
```

Wut.

Alright, this isn't actually a big deal.  I had just come from working on an RSA challenge where I was literally finding the same type of numbers.  This was just more of that.  I decided to write a script for this challenge which utilizes a new site I had just discovered.  This new site gives you __A__ and __B__ given __C__ such that __C = A^B__, which is what we want.  The script worked and I got the flag.  I felt pretty good about my solution, too.  Until I read another person's solution.

In my script, if the website didn't return any numbers (for some reason), the script would pause to allow the user to manually submit numbers or else he could type 'none' if the only possible solution was __1__ and __C__.  After all, that is a totally legitimate answer.  The server accepted those answers, too.  So why did my script make 100 requests to a third party website when it could just __submit 1 and the given C number for every iteration__?!

That was someone else's solution.  Simple.  Don't overthink.

My solution is below.  It worked, it's just...  Overly complicated to say the least.

### Script (Python)

```python
import socket
import urllib
import urllib2
import re
import time

# CTF Challenge Connection
TCP_IP = '91.231.84.36'
TCP_PORT = 9988
BUFFER_SIZE = 16384  # these numbers are freaking huge, but this huge?

# Website Connection
URL = 'http://factordb.com/index.php?'

# Connect to CTF Challenge
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((TCP_IP, TCP_PORT))
print 'Connecting to ', TCP_IP, ':', TCP_PORT

# Loop through challenges until there are none left
i = 1
while 1:
	
	# Reset URL each iteration
	URL = 'http://factordb.com/index.php?'

	# Sleep for 4 seconds so network doesn't get congested
	time.sleep(4)

	# Get new data
	data = s.recv(BUFFER_SIZE)

	# Final iteration, print flag and leave while loop
	if i == 100:
		print data
		break
	
	# Regex for only the number
	new_number = re.search(r'(C =\s*)(\d+)', data)

	# Get new A and B numbers
	query = urllib.urlencode({'query': new_number.group(2)})
	URL += query

	# Try to automatically find the A and B numbers
	try:
		response = urllib2.urlopen(URL)
		result = response.read()

		# factors is the wrong word, but I can't think of the correct word
		factors = re.findall(r'\(<a href="index.php\?id=\d+"><font color="#\d+">(\d+)<\/font><\/a>\)\^(\d+) =', result)
		if factors:
			answer1, answer2 = factors[0]
		else:
			answer1 = new_number.group(2)
			answer2 = 1
		final = str(answer1) + ' ' + str(answer2) + '\r\n'

	# Allow user to manually assign A and B numbers
	except:
		print new_number.group(2)
		key_input = raw_input('Type "A" Number (or type "none")>')
		if key_input == "none":
			final = str(new_number.group(2)) + ' 1'
		else:
			answer1 = key_input
			answer2 = raw_input('Type "B" Number>')
		final = str(answer1) + ' ' + str(answer2) + '\r\n'
	
	s.send(final)
	i += 1
s.close()
```

### Flag

`h4ck1t{R4ND0M_1S_MY_F4V0UR1T3_W34P0N}`