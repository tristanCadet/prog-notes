# Security

#### Generating a secure random string

Note: most of the following is based on Wikipedia's &mdash; *[Random password generator][https://en.wikipedia.org/wiki/Random_password_generator]* &mdash; and linked articles.  

##### Common pitfalls

- Using third-party programs without investigating their safety:

> While there are many examples of "random" password generator programs available on the Internet, generating randomness can be tricky and many programs do not generate random characters in a way that ensures strong security.

> Furthermore, and probably most importantly, transmitting candidate passwords over the Internet raises obvious security concerns, particularly if the connection to the password generation site's program is not properly secured or if the site is compromised in some way. 

- Using time as a seed:

> There are about 31 million seconds in a year, so an attacker who knows the year (a simple matter in situations where frequent password changes are mandated by password policy) and the process ID  that the password was generated with, faces a relatively small number, by cryptographic standards, of choices to test.

Sources such as user keyboard and mouse events can be used as seeds.

- Using a language's default random number generator instead of a crypto-secure one:

> All pseudo-random number generators have an internal memory or state. The size of that state determines the maximum number of different values it can produce: an *n*-bit state can produce at most $2^n$ different values. On many systems *rand* has a 31 or 32-bit state, which is already a significant security limitation. 

##### Password strength & Entropy

The password's strength against a brute-force attack can be obtained by computing the entropy $H=L\,\log_{2}N$  of its generating process ; with N the number of possible symbols and L the length of the password. Using a $log_{2}$ scale gives us the equivalent number of random bits we would have to generate to get this entropy.

*A few entropies for different symbol sets and $L=1$*:

|                          Symbol set                          | Symbol count *N* | Entropy per symbol *H* |
| :----------------------------------------------------------: | :--------------: | :--------------------: |
|                             0–9                              |        10        |       3.32 bits        |
|                       Hex (0-9, A-F )                        |        16        |         4 bits         |
|                        a–z, A–Z, 0–9                         |        62        |       5.95 bits        |
|                  ASCII printable characters                  |        95        |       6.55 bits        |
| [Diceware](https://en.wikipedia.org/wiki/Diceware) word list |       7776       |       12.9 bits        |

> A password generated using a 32-bit generator is limited to 32 bits entropy, regardless of the number of characters the password contains.

##### Some brute-force safe algorithms (in Javascript) 

With Javascript:

```javascript
function generate(length = 12) {
    var uppercase = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
    var lowercase = 'abcdefghijklmnopqrstuvwxyz';
    var numbers = '0123456789';
    var symbols = '!"#$%&\'()*+,-./:;<=>?@^[\\]^_`{|}~';
    var all = uppercase + lowercase + numbers + symbols;
    var password = '';
    var rands = new Uint8Array(length);
    window.crypto.getRandomValues(rands);
	rands.forEach(rand => {
        password += all[Math.floor(rand/256 * all.length)];
    })
    return password;
}
```

With $L=12$ and $N=95$, this algorithm has an entropy $H=12\,\log_{2}95\approx78.84$ bits

Or with the *Node.js* *crypto* library:

```javascript
const crypto = require('crypto')
function generate(length = 32) {
	return crypto.randomBytes(length).toString('hex')
}
```

We generate 32 bytes i.e. 256 bits randomly, which means $H=256$ bits (and matches the formula with $L=256$ and $N=2$; $H=256\,\log_{2}2=256$  bits).