rbytes
======

> Generates cryptographically secure random byte sequences

rbytes generates cryptographically secure random byte sequences using native bindings to OpenSSL's [pseudo random number generator](http://www.openssl.org/docs/crypto/rand.html). Use rbytes to generate session keys, UUIDs or anything else that requires fast generation of blocks of random data.

Synopsis
--------

Create a buffer holding 16 random bytes:

    var rbytes = require('rbytes');

    var rbuff = rbytes.randomBytes(16);
    // <Buffer 69 5d 5d f6 42 04 1b 86 f2 77 5d 2b 4f 0f 72 26>

rbytes adds two convenience methods to Node's Buffer class for easy conversion between Buffers and hex strings:

    rbuff.toHex();
    // '695d5df642041b86f2775d2b4f0f7226'

    var buff = Buffer(1);
    buff.writeHex('f);
    // <Buffer 0f>

    buff.writeHex('g);
    // TypeError: Invalid hex string

Installation
------------

    $ npm install rbytes

rbytes requires node version 0.3.0 or higher.

Notes
-----

rbytes binds to OpenSSL's [RAND_bytes](http://www.openssl.org/docs/crypto/RAND_bytes.html) function, which generates cryptographically strong pseudorandom bytes. This function does not block, however it will throw an error if there isn't enough random seed data on your system. Support is planned for RAND_pseudo_bytes, which are guaranteed to be available at the cost of being (potentially) less secure.

Simple random number generation (like Math.rand()) is planned for a future version.