  # PHP Security Functions

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



<br><br>



Other resources:

https://searchsecurity.techtarget.com/definition/MD5

http://php.net/manual/en/faq.passwords.php#faq.passwords.fasthash

https://stackoverflow.com/questions/2640566/why-use-sha1-for-hashing-secrets-when-sha-512-is-more-secure

https://en.wikipedia.org/wiki/SHA-2

