# demonet

<br>

## Authentication



### Hashing a password

"*Hashing*" a password refers to taking a plain text password and putting it through a [hash function](https://en.wikipedia.org/wiki/Hash_function). The hashing algorithm takes in a string of any size and outputs a fixed-length string. No matter the size of the original string (i.e., the plain text password), the output (the hash) is always the same length. Since the same process is always applied, the same input always yields the same output.

Say the plain text password is `P!zz4p13`. Every time `P!zz4p13` is passed into the hash function, the returned hash is the same.

Say another plain text password is `Ch33z7Br3@d!` which happens to be 4 characters longer than `P!zz4p13`. Regardless of the password's length, the length of the hash produced for both passwords will be the same. The exact length depends on the algorithm.

Because hash functions always produce the same result for a specific input, they are predictable. This means an attacker could figure out the original password from the hash. In other words, hashing the password is not enough.

<br>

### Salting a password

A "*salt*" is a random string. By hashing a plain text password with a generated salt, the hash algorithm is no longer predictable. The same password, once hashed, will no longer yield the same hash again without using the same salt. Salts also help mitigate [hash table](https://en.wikipedia.org/wiki/Hash_table) attacks by forcing attackers to re-compute them using the salts for each user.

<br>

### Choosing a cryptographic hash function for storing passwords

To qualify as a [cryptographic hash function](https://en.wikipedia.org/wiki/Cryptographic_hash_function), the hashing algorithm must be "*pre-image resistant*" and "*collision resistant*".
	
- a hash function is pre-image resistant if it is computationally infeasible to find any input that hashes to a known output; i.e. given y, it is difficult to find an x such that hash(x) = y
	
- a hash function is collision resistant if it is highly-improbable that any two inputs share an identical hash

Rapidly evolving hardware must be accounted for especially when the length of passwords remain constant. Therefore, it is desirable for the hash function to take in parameters which allow adaptation to future faster hardware.

[Bcrypt](https://en.wikipedia.org/wiki/Bcrypt) is such a hash function. Bcrypt's salted hash meets current [cryptographic security standards for the web](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html#bcrypt) and is an optimal solution to store passwords for a web application. 

#### Side notes and alternative hash functions
- Why Bcrypt is [better than SHA-256 for storing passwords](https://codahale.com/how-to-safely-store-a-password/).
- Argon2 won the 2015 [Password Hashing Competition](https://www.password-hashing.net/). Argon2id is recommended as a better alternative to Bcrypt for newer systems. 
- [PBKDF2](https://en.wikipedia.org/wiki/PBKDF2) received approval by NIST and has validated FIPS-140 compliance. However, Bcrypt is generally preferred as it holds up better with GPU/ASIC attacks than PBKDF2 with similar inputs.

### Bcrypt hash function

    hash = bcrypt(password, salt, workFactor)

where:
- `password` is a strong pasword
- `salt` is a long random unique value
- `workFactor` is the appropriate value that is relative to the hardware and security requirements
