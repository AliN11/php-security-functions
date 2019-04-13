  # PHP Security Functions

*Updating...*

A complete guide to PHP hash and encryption functions

I'll answer these questions for each items:

  - What is it?
  - How to use it?
  - When to use it?
  - When not to use it?



  ## MD5
**What is it?**

It is a **one-way** cryptographic function that accepts a message of **any length** as input and returns as output a **fixed-length** (128 bit) digest value to be used for authenticating the original message.



<br>



**How to use it?**

  ```php
md5 ( string $str [, bool $raw_output = FALSE ] ) : string
  ```

If the optional `$raw_output` is set to true, the plain binary string of the hash will be returned. This is only useful if you need to store or transfer the hash in a binary format.  [🔗](https://stackoverflow.com/a/7811439/3578287)

  ```php
  $str = 'I love you';

  $hash = md5($str); // e4f58a805a6e1fd0f6bef58c86f9ceb3
  $hash = md5($str, true); // ����Zn�������γ
  ```



<br>



**When to use it?**

For non-security cases, e.g. generating random string for file names. 



<br>



**When not to use it?**

As php.net says, it is not recommended to use md5 to secure passwords:

  >  Hashing algorithms such as MD5, SHA1 and SHA256 are designed to be very fast and efficient. With modern techniques and computer equipment, it has become trivial to "brute force" the output of these algorithms, in order to determine the original input.
  >
  >  Because of how quickly a modern computer can "reverse" these hashing algorithms, many security professionals strongly suggest against their use for password hashing.



<br>



  ## SHA1

**What is it?**

It is a **one-way** cryptographic function that accepts a message of **any length** as input and returns as output a **fixed-length** (160 bit) digest value to be used for authenticating the original message. It is more secure but slower than MD5



<br>



**How to use it?**

  ```php
sha1 ( string $str [, bool $raw_output = FALSE ] ) : string
  ```
The optional `$raw_output` is similar to [MD5](https://github.com/AliN11/php-security-functions#md5).

  ```php
$str = 'I love you';

$hash = sha1($str); // ce48c9870c7ae19796438aed65458c8bdc335157
$hash = sha1($str, true); // �HɇzᗖC��eE���3QW
  ```



<br>



**When to use it**

For non-security cases, e.g. generating random string for file names. 

Not all hash uses are security-related. Git uses SHA1 to cheaply distinguish between objects. In that case, because the possibility of collision between two documents is incredibly small with SHA1, there really is no justification for the additional space requirement of SHA512 when SHA1 is more than suitable for the task. [🔗](https://stackoverflow.com/a/2640600/3578287) [🔗](https://stackoverflow.com/questions/2640566/why-use-sha1-for-hashing-secrets-when-sha-512-is-more-secure#comment2655203_2640566)



<br>



**When not to use it?**

Similar to [MD5](https://github.com/AliN11/php-security-functions#md5), it is not recommended to use SHA1 to secure passwords.



<br>



## SHA2 Family

**What is it?**

SHA-2 (Secure Hash Algorithm 2) is a set of cryptographic hash functions. The SHA-2 family consists of six hash functions that are 224, 256, 384 or 512 bits:

 SHA-224, SHA-256, SHA-384, SHA-512, SHA-512/224, SHA-512/256. [🔗](https://en.wikipedia.org/wiki/SHA-2)

They are **one-way** cryptographic function that accept a message of **any length** as input and return as output a **fixed-length** digest value.



<br>



| Function    | Output Length (Bits) |
| ----------- | -------------------- |
| SHA-224     | 224                  |
| SHA-256     | 256                  |
| SHA-384     | 384                  |
| SHA-512     | 512                  |
| SHA-512/224 | 224                  |
| SHA-512/256 | 256                  |



<br>



**How to use it?**

You can use them by php `hash` function:

```php
 hash ( string $algorithm , string $data [, bool $raw_output = FALSE ] ) : string
     
 // $algorithm may be: sha224, sha256, sha384, sha512, sha512/224, sha512/256
 // or other $algorithms that exists in hash_algos() function
```



<br>



**When to use it?**

They are general purpose hash functions. They are good only for non-security cases, e.g. generating random string for file names. 



<br>



**When not to use it?**

Similar to SHA1 and MD5, you should not use them for security cases such as hashing sensitive data. 

> General-purpose hashes have been obsolete for passwords for over a decade. The issue is that they're fast, and passwords have low entropy, meaning brute-force is very easy with any general-purpose hash. You need to use a function which is deliberately slow, like PBKDF2, bcrypt, or scrypt.  [🔗](https://security.stackexchange.com/a/90065/102970)


<br>


## Bcrypt

**What is it?**

Bcrypt is a password hashing function. Bcrypt is an adaptive function: over time, the iteration count can be increased to make it slower, so it remains resistant to brute-force search attacks even with increasing computation power. [🔗](https://en.wikipedia.org/wiki/Bcrypt)

Alert: When using bcrypt you should be aware that it limits your maximum password length to 50-72 bytes.



<br>



**How to use it?**

```php
$options = [
    'cost' => 12,
];

password_hash("password", PASSWORD_BCRYPT, $options);
```

This will always result in a hash using the `$2y$` crypt format, which is always 60 characters wide. `cost` parameter is used here to define how many iteration over the password should be performed. Higher cost, higher security, higher execution time.

As [php.net](https://www.php.net/manual/en/function.password-hash.php) says:

It is strongly recommended that you do not generate your own salt for this function. It will create a secure salt automatically for you if you do not specify one. Providing the salt option in PHP 7.0 will generate a deprecation warning. Support for providing a salt manually may be removed in a future PHP release.   

It is recommended that you test this function on your servers, and adjust the cost parameter 
so that execution of the function takes less than 100 milliseconds on interactive systems. See example #3 in the above link.



<br>



**When to use it?**

When security matters. When you would have uncrackable passwords.



<br>



**When not to use it?**

Bcrypt takes time and resources to generate (in comparison to MD5, SHA1, etc.). You can simply see the performance of generating Bcrypt vs SHA1 in a `for` loop. So if you would hash a string in which security doesn't matter, do not use Bcrypt. Use fast hashing algorithms.



<br>



## Argon2

**What is it?**

Argon2 is a password-hashing function that can be used to hash passwords for credential storage, key derivation, or other applications.

Argon2 has three variants: Argon2i, Argon2d, and Argon2id.

Argon2d is faster and uses data-depending memory access, which makes it highly resistant against GPU cracking attacks and suitable for applications with no threats from side-channel timing attacks (eg. cryptocurrencies). 

Argon2i uses data-independent memory access, which is preferred for password hashing and password-based key derivation, but it is slower as it makes more passes over the memory to protect from tradeoff attacks

Argon2id is a hybrid of Argon2i and Argon2d, using a combination of data-depending and data-independent memory accesses, which gives some of Argon2i's resistance to side-channel cache timing attacks and much of Argon2d's resistance to GPU cracking attacks.  [🔗](https://github.com/p-h-c/phc-winner-argon2)



<br>



**How to use it?**

```php
$options = ['memory_cost' => 2048, 'time_cost' => 4, 'threads' => 3];

// PHP 7.2.0+
password_hash("password", PASSWORD_ARGON2I, $options); // $argon2i$v=19$m=1024,t=2,p=2$dVBCdG9qbTdkN3dvSnpIcw$wXTxsa/LKAJGwk3+ZWXgfEx66Vs4R0JAMm7i3PNJ2wg


// PHP 7.3.0+
password_hash("password", PASSWORD_ARGON2ID, $options); // $argon2id$v=19$m=1024,t=2,p=2$aERwOTFDY2lPNUJZRDBoYw$VI2gLlJLzQZD3r9tYGszvN6uj2PZVuUv6Ukp7gcJ+dw
```

- `memory_cost` - Maximum memory (in bytes) that may be used to compute the Argon2 hash (default 1024)
- `time_cost` - Maximum amount of time it may take to compute the Argon2 hash (default 2)
- `threads` - Number of threads to use for computing the Argon2 hash (default 2)

<br>



**When to use it?**

Argon2i uses data-independent memory access. It is slow because it makes more passes over the memory to protect from trade off attacks. It is highly recommended for password hashing and password-based key derivation.



<br>



**When not to use it?**

As I described in [Bcrypt](https://github.com/AliN11/php-security-functions#bcrypt) section, if you would hash something in which security doesn't matter, do not use Argon2. Use fast hashing algorithms instead.



<br>



*Other functions coming soon ...*



Resources:

https://stackoverflow.com/a/47602045/3578287

https://github.com/p-h-c/phc-winner-argon2

https://searchsecurity.techtarget.com/definition/MD5

http://php.net/manual/en/faq.passwords.php#faq.passwords.fasthash

https://stackoverflow.com/questions/2640566/why-use-sha1-for-hashing-secrets-when-sha-512-is-more-secure

https://en.wikipedia.org/wiki/SHA-2

https://www.mscharhag.com/software-development/bcrypt-maximum-password-length

https://security.stackexchange.com/questions/39849/does-bcrypt-have-a-maximum-password-length
