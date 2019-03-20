# php-hash

I will 

I'll answer these questions for each items:

- What is it?
- How to use it?
- When to use it?
- When not to use it?



## MD5

##### What is it?

It is a **one-way** cryptographic function that accepts a message of **any length** as input and returns as output a **fixed-length** digest value to be used for authenticating the original message.

As php.net says, it is not recommended to use md5 to secure passwords

##### How to use it?



##### When to use it?



##### When not to use it?

As php.net says, it is not recommended to use md5 to secure passwords:

>  Hashing algoritms such as MD5, SHA1 and SHA256 are designed to be very fast and efficient. With modern techniques and computer equipment, it has become trivial to "brute force" the output of these algorithms, in order to determine the original input.
>
> Because of how quickly a modern computer can "reverse" these hashing algorithms, many security professionals strongly suggest against their use for password hashing.



Sources:

https://searchsecurity.techtarget.com/definition/MD5

http://php.net/manual/en/faq.passwords.php#faq.passwords.fasthash

