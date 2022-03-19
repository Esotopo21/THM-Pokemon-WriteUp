# THM-Pokemon-WriteUp

Write up for https://tryhackme.com/room/pokemon (Visit https://tryhackme.com for more)

# Find the Grass-Type Pokemon

Visiting port 80 (default HTTP port) I found the classic Apache2 server welcome page.
As in many other rooms there is something hide in this page, there are a pair of credentials written in html element.
Using those credentials I was able to ssh in to the server, investigating the user's home I found a zip file on the Desktop containing a text file
with an hex encoded message, decoding it gave me the grass-type pokemon.

# Find the Water-Type Pokemon

Actually I found this one at last, but I didn't need further exploitations as it was in /var/www/html contained in a text file and rotated by 14 positions, I decoded this message using a tool of my own by the way (https://github.com/Esotopo21/python-caesar-substitution)

# Find the Fire-Type Pokemon

By running find in the user's home I noticed something in the Video folder, at the end of the path there a "obfuscated" c++ code, no need to run it, just 
printed the content which gave me ash's credentials.
Switching user to ash I immediately noticed that there was something wrong: I coulnd't enter ash's home. This rang me a bell so I checked sudo's permissions

```
$ sudo -l -l
Matching Defaults entries for ash on root:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User ash may run the following commands on root:

Sudoers entry:
    RunAsUsers: ALL
    RunAsGroups: ALL
    Commands:
        ALL
```

So by simple running `sudo su` I was root.

Searching in the filesystem for something supicious I found a folder called why_am_i_here in /etc containing the base64 encoded answer for this question

# Who is Root's Favorite Pokemon?

As I stepped in the machine I noticed a file in /home which required root permission that I now have, root's favourite pokemon is there in plain text ... or should I say that the entire content of the file it's root's favourite ;)
