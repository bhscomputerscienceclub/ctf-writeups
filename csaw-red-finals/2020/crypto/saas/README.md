---
author: karmanyaahm
---

# SAAS

Looking through the [problem file](server.py), I tried to think about all possible vulnerabilities. It was clear that the verify function was pretty simple and had no implementation errors. That made me look into vulnerabilities with the part where it checked if the string "hocus pocus" was in the text.

I [searched for RSA signature vulnerabilities vulnerabilities](https://duckduckgo.com/?t=ffab&q=rsa+signature+vulnerabilities&ia=web) and found the third result talking about a `blinding attack`. Reading through [the article](https://masterpessimistaa.wordpress.com/2017/07/10/blinding-attack-on-rsa-digital-signatures/) I realized I had seen something like this before and set out to implement this attack.

I succesfully implemented the first part in sage and even got a signature back for `M'` but didn't know how to implement the rest.

```sage
sage: from Crypto.Util.number import bytes_to_long                                                    
sage: m = bytes_to_long(b"hocus pocus")                                                               
sage: mm = ((r^e)*m)%n                                                                                
sage: mm                                                                                              
43749591641576277187206310680046415835120891465996535989751289766274942137843271328264605192419304272872693128837647429500421233292982464515003568122550003591909317711114198519524245026477570460445130263674126158037752191385833585943499050560440046202234979066334420748876993523792041648079963478052583586310
sage: hex(mm)                                                                                         
'0x3e4d2e3868912620afc0e9bd91570a9f30c8084dcfa9d7e8b61ece1335fe985d88eb7f2f8d9e1cd3b39ae97c7db7891d09d70d5edd6a05e7c6754382149165c8213440a9073a77d6fd92eabf6068da917158ea7043ddd9ace38c5a267539567d0e80bed68d236614717e4d1b545f15464b9b09b35cd061469744cb1296fd3a06'
sage: s = int('8fa957ccd2df8267ef4c263fef2c520ae074ab5678a0ffe948fd0f88692438849f98cd51615228bb409538a
....: 33df87adf9d02eb5f7e5a7db469516e410c73bfd67c13743d34d8c67968a12feaacd4323ec499a4fbd0a11c7a5cd96da
....: 50d595a4463953ded688f7cef05de83c805b73c8bbad7e4e0162e389e73e6c727df3c35d2',16)                  
sage: s                                                                                               
100882533224562798434591942527636286222770282414829785256748648987094920701900368543541437543511348313394164788681585487304175387647389557730879242841689276094670036262233336302678774924432749470416842023051569345557948795004884791203530624874890385295859515582931768459559534803148801981175222695414556538322
```

So, I looked for examples of this implemented in Python on GitHub and after a few that didn't work, I came across [this](https://github.com/ashuanindian/Blind-Signature/blob/master/RSA/blind.py) very well implemented script.

I imported its functions into a python interpreter and did the things in <py.py> (warning messy since on the python REPL) and got the signed string "hocus pocus".
Submitting that to the server gives the flag.

TL;DR - Blinding Signature Attack
