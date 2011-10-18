Password based key-derivation function - PBKDF2

To use this in your application, simply download the
module, then run something like this:

    import pbkdf2
    import hashlib
    import os

    >>> pbkdf2.pbkdf2(hashlib.sha256, b"password1", os.urandom(32), 32000, 16)
    b'\x1e\xa9\xa0\xa7N\xf6\x97\x9ce\x94ZpU\x03n?'


PBKDF2, from PKCS #5 v2.0:
    <http://tools.ietf.org/html/rfc2898>

For proper usage, see NIST Special Publication 800-132:
    <http://csrc.nist.gov/publications/PubsSPs.html>

The arguments for this function are:

 - `digestmod`
    a crypographic hash constructor, such as hashlib.sha256
    which will be used as an argument to the hmac function.
    Note that the performance difference between sha1 and
    sha256 is not very big. New applications should choose
    sha256 or better.

 - `password`
    The arbitrary-length password (passphrase) (bytes)

 - `salt`
    A bunch of random bytes, generated using a cryptographically
    strong random number generator (such as os.urandom()). NIST
    recommend the salt be _at least_ 128bits (16 bytes) long.

 - `count`
    The iteration count. Set this value as large as you can
    tolerate. NIST recommend that the absolute minimum value
    be 1000. However, it should generally be in the range of
    tens of thousands, or however many cause about a half-second
    delay to the user.

 - `dk_length`
    The lenght of the desired key in bytes. This doesn't need
    to be the same size as the hash functions digest size, but
    it makes sense to use a larger digest hash function if your
    key size is large. 
