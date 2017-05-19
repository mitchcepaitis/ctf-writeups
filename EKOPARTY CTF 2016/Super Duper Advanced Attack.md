# Super Duper Advanced Attack

### Challenge
- **Competition:** EKOPARTY CTF 2016
- **Category:** Web
- **Points:** 100

> Can you find the flag?
>
> http://0491e9f58d3c2196a6e1943adef9a9ab734ff5c9.ctf.site:20000


### Solution

Upon visiting the challenge page, it looked like a SQL injection vulnerability may exist.  After a bit of experimenting, I was able to successfully determine and display the number of columns in the query on the page:

```none
'UNION(SELECT(1),2);-- -
```

Further, I was able to display to software version information:

```none
'UNION(SELECT(@@VERSION),2);-- -
5.7.15-0ubuntu0.16.04.1
```

I explored the current __users__ table and dumped login names and passwords, which proved useless for this challenge.  I tried searching for other tables, but nothing held relevant information.  After a while, the challenge admins released a clue which ultimately pointed me in the right direction.  I first tried looking for a global variable with the flag (globals have @@ in front of their names), which was unsuccessful:

```none
'UNION(SELECT(@@FLAG),2);-- -
```

Finally, I looked at the potential local variable with the flag information in it (locals have a single @ in front of their names):

```none
'UNION(SELECT(@FLAG),2);-- -
```

Success!  The flag was in fact stored in this local variable.


### Flag

```none
EKO{do_not_forget_session_variables}
```