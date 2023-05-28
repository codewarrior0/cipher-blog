---
title: "Solutions to Feynman Ciphers #2 and #3"
date: 2023-05-27
---
### Background
During the 1940s, the scientists who worked on the atomic bomb at Los Alamos also amused each other by exchanging encrypted messages. Five of these messages, or "ciphers", were eventually made public and solved, decades after they were first encrypted. 

Two of them found their way onto Reddit and were known to be created by mathematician Paul Olum and given to physicist Richard Feynman as a challenge, giving them the name "Olum Ciphers".  [Olum 1](https://www.reddit.com/r/codes/comments/b69ovn/feynman_olum_i_cipher/) was posted to Reddit in 2019, and [solved by Paul Relkin](https://www.researchgate.net/publication/356203267_Solving_the_Olum_1_Cipher), revealing a quote about the laboratory's mail procedure, enciphered with a simple substitution with null letters periodically inserted. [Olum 2](https://www.reddit.com/r/codes/comments/b69xtq/feyman_olum_ii_cipher/) was also posted in 2019, but its solution had to wait another month for Paul Relkin (again!) to invent a [completely new method for diagnosing transposition ciphers](https://www.researchgate.net/publication/357106780_Solving_the_Olum_2_cipher_a_new_approach_to_cryptanalysis_of_transposition_ciphers), which helped him to decipher a keyed columnar transposition with a shifting key.  (I am very grateful to Mr. Relkin for sharing his methods! His transposition analyzer has come in handy on more than one occasion.)

Three of them were received by Richard Feynman from an anonymous researcher and later [posted on Usenet's sci.crypt](https://ciphermysteries.com/other-ciphers/feynman-ciphers) in 1987. Cipher enthusiasts called them the "Feynman Ciphers". The first of the three ciphers was solved by Jack C. Morrison and revealed to be a simple unkeyed transposition cipher, concealing a passage from The Canterbury Tales in Middle-English.

The ciphers Feynman #2 and Feynman #3 remained unsolved until I had solved them just a few days ago. I will be happy to present the decipherments, describe the cipher method, and explain the process that led to the solution.

### Feynman #2 

Ciphertext:
```
XUKEXWSLZJUAXUNKIGWFSOZRAWURORKXAOSLHROB
XBTKCMUWDVPTFBLMKEFVWMUXTVTWUIDDJVZKBRMC
WOIWYDXMLUFPVSHAGSVWUFWORCWUIDUJCNVTTBER
TUNOJUZHVTWKORSVRZSVVFSQXOCMUWPYTRLGBMCY
POJCLRIYTVFCCMUWUFPOXCNMCIWMSKPXEDLYIQKD
JWIWCJUMVRCJUMVRKXWURKPSEEIWZVXULEIOETOO
FWKBIUXPXUGOWLFPWUSCH
```

Plaintext:

> Why, if 'tis dancing you would be,  
> There is [sic] brisker pipes than poetry.  
> Say, for what were hop-yards meant,  
> Or why was Burton built on Trent?  
> Oh many a peer of England brews  
> Livelier liquor than the Muse,  
> And malt does more than Milton can  
> To justify God's ways to man.  
> Ale, man, ale's the stuff to drink  
> For fellows whom it hurts to think

From [*Terence, This is Stupid Stuff*](https://stuff.mit.edu/people/dpolicar/writing/poetry/poems/terence.html) by A.E. Housman, 1896.

### Feynman #3

Ciphertext:
```
WURVFXGJYTHEIZXSQXOBGSVRUDOOJXATBKTARVIX
PYTMYABMVUFXPXKUJVPLSDVTGNGOSIGLWURPKFCV
GELLRNNGLPYTFVTPXAJOSCWRODORWNWSICLFKEMO
TGJYCRRAOJVNTODVMNSQIVICRBICRUDCSKXYPDMD
ROJUZICRVFWXIFPXIVVIEPYTDOIAVRBOOXWRAKPS
ZXTZKVROSWCRCFVEESOLWKTOBXAUXVB
```

Plaintext:
> The behavior of liquid helium, especially below the lambda transition, is very curious. 
> The most successful theoretical interpretations so far have been largely phenomenological.
> In this paper and one or two to follow, the problem will be studied entirely from first principles.

From [*Atomic Theory of the lambda Transition in Helium*](https://authors.library.caltech.edu/3537/1/FEYpr53b.pdf) by Richard Feynman, *The Physical Review*, 1953.


### Cipher method

Both of the challenges make use of the same cipher method. Two monoalphabetic substitutions, which could not be completely recovered, are used:

```
Plain:       ABCDEFGHIJKLMNOPQRSTUVWXYZ
Alphabet 1:  MANYREQUS.HVBCID.OLWGZX.K. 
Alphabet 2:  JHAZTENYXMLOCUFBQVKPSGW.D.
```

In this method, each word is enciphered by one of the two substitutions, alternating between the two after each word. The first word of each sentence (or line of poetry) is always enciphered using Alphabet 1, which leads to occasional cases of Alphabet 1 being used for two words in a row. Words having an even number of letters are written in reverse. 

The ciphers keep to this method with only a single exception: The successive words "England brews" are both enciphered with Alphabet 2, where "brews" ought to use #1.

```
Plain:       the behavior of liquid helium especially below
Alphabet 1:  WUR          IE        URVSGB            ARVIX
Alphabet 2:      HTYJGXFV    OXQSXZ        TKBTAXJOOD
Reversals:       VFXGJYTH EI ZXSQXO BGSVRU DOOJXATBKT
Combined:    WUR VFXGJYTH EI ZXSQXO BGSVRU DOOJXATBKT ARVIX

Plain:       why if tis dancing you would be // there is brisker pipes than poetry
Alphabet 1:  XUK    WSL         KIG       AR    WUROR    AOSLHRO       WUMC
Alphabet 2:      XE     ZJUAXUN     WFSOZ             XK         BXBTK      BFTPVD
Reversals:       EX                       RA          KX               WUMC DVPTFB
Combined:    XUK EX WSL ZJUAXUN KIG WFSOZ RA    WUROR KX AOSLHRO BXBTK CMUW DVPTFB
```

Alphabet 1 appears to be derived from a key-phrase beginning with the words 'MANY REQUESTS HAVE BEEN'. I don't know whether Alphabet 2 is systematically derived.

### Solve path

Letter frequency for both ciphers was neither polyalphabetic nor monoalphabetic. The overall Index of Coincidence was 0.045 for #2, and 0.042 for #3. (Note that a result of 0.038 is "random/polyalphabetic", while 0.066 is "monoalphabetic".) There were no telltale spikes in the plot of periodic Index of Coincidence. Repetitions were slightly more than expected by chance. A four letter repetition `SQXO` appeared in both ciphers, as did several three-letter ones. The graphs of letter frequency between the two were also similar enough for me to suspect that they shared a method.

This cipher sat in my "unsolved cases" file for months. I occasionally came back to prod at it using Vigenere encipherment or check the Kappa IOC between the two messages. The break-in finally came when I concatenated both ciphers, reversed the text, and fed it into [AZDecrypt](https://github.com/doranchak/azdecrypt) which produced this "decipherment":

> PRINCIPLES DS LESS ROT AT DELARS BE I BETS 
CAD ILL PARCE LIESTS ERRE I TOE ID ORATE 
BNAL AIO ITS I SET IN ATE PATE REVE A OR 
I LEAR ALCA AT SAME LOS SO STEE DAD A LILAD 
TEL A CITEROEST SMAAASSS MR TO STANDS ME 
EL MAMERIES TRANSITION RO PC SO ESTIE RACE 
SPECIALLINAR EMP LIVE I BE SHE SAM I OR AND 
HT END TO SD LMN IT IN EPS DOLLES LESS NIRB 
DES SETS AND I SAR ON A TAR ON AT DED A IS 
VESS IS ITS EODE TO AT IL TOND NOT TO RESEAST 
ALT STOP MS AEST D NOT LIVE OR RE BARE ALS 
DER HBN A LANE AS PEER A TAN I END TAL DON 
DREM CHER TON SO I IS DELD TO APS BRAI I 
ENDERE I NOD ROS SO SPOET RID NOT SEP I PLAH 
SELC IS AL AND CABLE OD MES AN ICN ABSE DISS 
NI

The first word `PRINCIPLES` jumped out at me. Past experience (plus the solution to Olum 1) had taught me that for some kinds of ciphers, a very partial solution of only a few words from an autosolver can lead to a complete break-in. I also had `TRANSITION` in the middle, a `SPECIALL` that comes right after an `E`, and a suspicious word-like `CITEROEST`.

I began solving it as a simple substitution, inserting the cribs `PRINCIPLES`, `TRANSITION`, and `ESPECIALLY` in the correct places to see what else comes out. This gave me the fragment `LACITER`. After a few moments, I remembered that I had originally reversed the text and thought of words that contain `RETICAL`... how about `THEORETICAL`? With the T and H, I saw short words like `THEY` and `HAVE` mixed in with obvious nonsense, so I wasn't ready to trust them yet, but I also saw `ROI.AHE.` at the very beginning, and `BEHAVIOR` seems like it belongs in the same paragraph as the other words I had assumed. With this many long words that seemingly belong together, one of them even *reversed* with respect to the others, I knew I was on the right track.

I spent a bunch of time trying to solve it as a homophonic substitution combined with a transposition, assuming multiple letters for `E A I T` and writing the text in various directions, but I couldn't get more than a few more short, untrustworthy words. At one point I assumed a Q and a U and got out `LIQUID` in one cipher and `LIQUOR` in the other, which was surprising.

During a trip to the grocery store, I thought about the IOC of about 0.045 again, and wondered whether it was actually homophonic, or just very mildly polyalphabetic with only two or three alphabets. Given the low complexity of the three solved ciphers, I didn't think a homophonic cipher or an obscure route transposition fit with the others. Thinking about different alphabets, I looked at the letters following `THEORETICAL`, which were `SCWRODORWNW`, whose repeated letters paint a big bulls-eye. A pattern search for `SCWRODORW` turned up `INTERPRET`, the word `INTERPRETATIONS` completed itself, and the cipher fell apart after that.
