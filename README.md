Encryption in a browser
=======================

Demonstration how public key encryption could work in a broswer.  Its based on the [jsencrypt](https://github.com/travist/jsencrypt) java library.

[DEMO](http://coder36.github.io/jsencrypt)


Notes
=====

Generating openssl keys
-----------------------

    openssl genrsa -out private_key.pem 4096
    openssl rsa -in private_key.pem -pubout > public_key.pem

The public key, is then made widely available for encyption.  Guard the private key with your life.  It should never leave the server on which it was generated.

Encryption
----------
 
    echo "mysecretpassword" | openssl rsautl -encrypt -pubin -inkey public_key.pem | base64 > t.enc

Decryption
----------

    cat t.enc | base64 --decode | openssl rsautl -decrypt -inkey dev.pem


Identity function
-----------------

    echo "mysecretpassword" | openssl rsautl -encrypt -pubin -inkey dev_pub.pem | base64 | base64 --decode | openssl rsautl -decrypt -inkey dev.pem


I need entropy NOW!
===================
During key generation, there may be a lack of entropy! - if this happens then the key generation appears to hang.  To generate additional entropy:

    yum install -y rng-tools
    sudo rngd -r /dev/urandom





