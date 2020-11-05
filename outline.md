# Post-quantum cryptography
## Problem:
Assymetric-encryption systems vulnerable to quantum computers.
The key-exchange in TSL relies on this (RSA, diffie-helman), and thus a new scheme is required.
Interesting point: for communication in which forward secracy was not used, an advisary could store that (encrypted) communication and simply wait for quantum computers to become available.
At that point, it would simply be a matter of cracking the key-exchange, and then find the symmetric encryption key used in the communication itself (probably AES).


1. How encryption works now
2. Why it is vulnerable to attacks from quantum computers
3. When will this be a real threat?
4. NISTs efforts to find a new standard for post-quantum encryption
5. The issue of non-forward secret communication.

## 1
At its core, all communication over the internet is essentially like shouting to each other in an crowded environment, open for anyone to hear.
At the infancy of the internet, this was fine, as the communication was only between trusted parties.
Today the situation is rather different, with personal details, photos, banking details, business secrets, and much more being transported over the internet.
The answer is the Transport Security Layer (TSL), which provides both authentication and encryption.
Authentication is the process of verifying the identity of the parties involved in the communication.
Encryption is the process of obfuscating the information in the communication, so that it is unreadable to anyone except the intended recipient(s).
There is an inherent issue with encryption over the web - how does the two parties, who have never met in person, establish a secure connection that is obfuscated for anyone else, when the establishment of such communication must happen over open communication?

The answer is of course asymmetric encryption, such as Diffie-Hellman(footnote: technically, it may be argued whether DH is asymmetric, but it undoubtedly provides a public-key protocol) and RSA.
The problem with asymmetric encryption is that it is slow, about 10'000 times slower (find source, obviously).
So the obvious solution is to use the asymmetric protocol no negotiate a symmetric key to be used for the rest of the communication.
This process of using asymmetric encryption to negotiate a symmetric key is known as _key exchange_.

Note: clarify what symmetric and asymmetric communication is.

## 2
It is this stage, the key exchange, that is vulnerable to quantum attacks.
The most used algorithms for key exchange today are dependent on the fact that the integer factorization problem is hard to solve (footnote: actually, the hidden subgroup problem for finite Abelian group).
As a practical example, consider the following written by the mathematician William Jevons in 1874:
> Can the reader say what two numbers multiplied together will produce the number 8616460799?[12] I think it unlikely that anyone but myself will ever know.
> 
> - William Stanley Jevons, 1874
Now, the answer is $89681 \times 96079$, which is not difficult to find with modern computers.
However, the concept stands: given two primes a and b, it is simple to compute N = axb.
However, if a and b are sufficiently large, it is extremely hard to find a and b given only N.
That is not the case for quantum computers, however.
Shor's algorithm can solve this problem in logarithmic time!
This threatens the integrity of modern encryption!

## 3.
How long until this is a realistic threat?
As of now, there exists no quantum computers powerful enough to factorize even trivially large numbers.
The current record on a quantum computer using Shor's algorithm is 21 (3x7) (footnote: this is not the largest number factorized by quantum computers, that would be 56153. But that is using another algorithm, which is not fast for large numbers).

## 4.
It is obvious that a post-quantum secure encryption standard has to rely on some different mechanism than the current standards -- that rely on the integer factorization problem.
As is common in cryptography research one tries to find methods that can be shown to reduce to known mathematical problems, for which there exist no known fast algorithm -- just like one did with the reduction of RSA and Diffie-Hellman into the hidden subgroup problem (integer factorization)).
In 2016 the National Institute of Science and Technology (NIST) initiated a standardization process for finding new methods of authentication an key exchange for the post-quantum era.
This process has gone through several rounds of discarding some submissions and moving on with the most promising.
As late as July 2020 the third round was announced, making this a very relevant topic.
In the third round seven submissions remain, four schemes for key exchange and three for authentication.

## 5.
Another interesting issue to consider in this context is the security of today's communication from future attack.
An adversary could in theory record vast amounts of encrypted communication today, knowing that the information will be possible to decrypt when powerful quantum computers are available.
There are two conclusions to be drawn from this notion.
1) all communication that has been or is going to be encrypted with vulnerable schemes, must be regarded as theoretically compromised.
2) post-quantum encryption standards are not something that need only be in place before the introduction of powerful quantum computers, they are needed as soon as possible.
All information currently being encrypted using vulnerable schemes is ultimately vulnerable to a sufficiently resourceful or specifically interested adversary.



## List of literature:
- https://www.nist.gov/news-events/news/2020/07/nists-post-quantum-cryptography-program-enters-selection-round
- 

- https://www.nist.gov/news-events/news/2020/07/nists-post-quantum-cryptography-program-enters-selection-round
- https://phys.org/news/2014-11-largest-factored-quantum-device.html
- https://arxiv.org/abs/1411.6758
