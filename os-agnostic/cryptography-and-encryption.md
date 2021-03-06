# Cryptography & Encryption

## Cryptography

{% embed url="https://pequalsnp-team.github.io/cheatsheet/crypto-101" %}

## Ciphers

[https://www.boxentriq.com/code-breaking](https://www.boxentriq.com/code-breaking) &lt;-- useful site which can help identify type of cipher. 

[https://www.dcode.fr](https://www.dcode.fr) &lt;-- one of the best sites I have found with many decoders for many types of ciphers.

[Cyber Chef](https://gchq.github.io/CyberChef/) &lt;-- very useful for chained ciphers which require different steps to solve. Can decrypt certificates.

### Fernet

Fernet \(symmetric encryption\) - **looks like base64** but decodes to garbage, in two parts. First part \(32 bytes\) is the key. Uses 128-bit AES in CBC mode and PKCS7 padding, with HMAC using SHA256 for authentication. IV is created from `os.random()`.

Decode fernet @ [https://asecuritysite.com/encryption/ferdecode](https://asecuritysite.com/encryption/ferdecode) &lt;-- Will also give the IV and timestamp \(could be useful!\) more info about this @ [https://cryptography.io/en/latest/fernet](https://cryptography.io/en/latest/fernet)

```python
from cryptography.fernet import Fernet

key = Fernet.generate_key()
f = Fernet(key)
token = f.encrypt(b"this is my key")
print('the key is ' + key + '/nThe cipher text is ' + token)
==========decrypt
from cryptography.fernet import Fernet
key = 'input key here'
f = Fernet(key)
token = 'cipher text here'
print(f.decrypt(token))
```

### Malbolge

Esoteric inferno encryption. Used in some CTF challenges. Malbolge programming language - **text from base64 looks like random text**, but complete garbage \(much of it unprintable.\) . Read for at [https://en.wikipedia.org/wiki/Malbolge](https://en.wikipedia.org/wiki/Malbolge) and [https://www.tutorialspoint.com/execute\_malbolge\_online.php](https://www.tutorialspoint.com/execute_malbolge_online.php)

## Test for Plaintext Output from a \(Python\) Script

```python
#checks the output from crypto and sees if at least 60% is ascii letters and returns true for possible plaintext
def is_plaintext(ptext):
    num_letters = sum(map(lambda x : 1 if x in string.ascii_letters else 0, ptext))
    if num_letters / len(ptext) >= .6:
      return True
```

## Digital Certificates

X.509

[https://8gwifi.org/PemParserFunctions.jsp](https://8gwifi.org/PemParserFunctions.jsp) -- extract information from various digital certificates

## Encryption/Decryption

[CyberChef](https://gchq.github.io/CyberChef/): Website for encryption/decryption of many different types at same time

good cipher tools: [http://rumkin.com/](http://rumkin.com/)

one time pad: `pt - ct = key`

decrypt rsa private key: `openssl rsautl -decrypt -inkey <key_file> < <pass.crypt (hex file?encrypted contents of pub key?)>`

* [Ippsec:HacktheBox - Charon](https://www.youtube.com/watch?v=_csbKuOlmdE)

`hydra -e nsr` - additional checks, "n" for null password, "s" try login as pass, "r" try the reverse login as pass

