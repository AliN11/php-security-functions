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



**When to use it?**

For non-security cases, e.g. generating random string for file names. 



**When not to use it?**

As php.net says, it is not recommended to use md5 to secure passwords:

>  Hashing algorithms such as MD5, SHA1 and SHA256 are designed to be very fast and efficient. With modern techniques and computer equipment, it has become trivial to "brute force" the output of these algorithms, in order to determine the original input.
>
>  Because of how quickly a modern computer can "reverse" these hashing algorithms, many security professionals strongly suggest against their use for password hashing.



## SHA1

**What is it?**

It is a **one-way** cryptographic function that accepts a message of **any length** as input and returns as output a **fixed-length** (160 bit) digest value to be used for authenticating the original message. It is more secure but slower than MD5



**How to use it?**

```php
sha1 ( string $str [, bool $raw_output = FALSE ] ) : string
```

The optional `$raw_output` is similar to [MD5](https://github.com/AliN11/php-security-functions#md5).



**When to use it**

For non-security cases, e.g. generating random string for file names. 

Not all hash uses are security-related. Git uses SHA1 to cheaply distinguish between objects. In that case, because the possibility of collision between two documents is incredibly small with SHA1, there really is no justification for the additional space requirement of SHA512 when SHA1 is more than suitable
for the task.  [🔗](https://stackoverflow.com/a/2640600/3578287) [🔗](https://stackoverflow.com/questions/2640566/why-use-sha1-for-hashing-secrets-when-sha-512-is-more-secure#comment2655203_2640566)



**When not to use it?**

Similar to [MD5](https://github.com/AliN11/php-security-functions#md5), it is not recommended to use SHA1 to secure passwords.

Sources:

https://searchsecurity.techtarget.com/definition/MD5

http://php.net/manual/en/faq.passwords.php#faq.passwords.fasthash

https://stackoverflow.com/questions/2640566/why-use-sha1-for-hashing-secrets-when-sha-512-is-more-secure