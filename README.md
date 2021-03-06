Cryptic-Auth
============

Simple, and Dev friendly public/private key authentication for the web (and anything else)

* Client has Chrome Plugin or Firefox Add-On installed (Open Source)
* Server implements Library that facilitates Pub/Private Transaction for Auth (Open Source)



Problem
-------

There are too many applications that require a user/pass combination. With so many passwords it's natural to reuse a couple.

Solutions?
----------

OAuth?

* It works, but it is a huge pain to setup; which, unfortunately, hinders it's widespread use.
* Client still needs to login with OAuth Provider

Pub/Priv?

* If it can be packaged well it would be cinch to setup. 
* Client never sends a password! One click login!
* Server doesn't need to store passwords, only public keys (heck you can put it in a plain text file for everyone to see, and still be golden!)

Pub/private Keys for the web

How It Works
============

Client
------

* Have the plugin installed and setup keys (with or without a password just like ssh keys)
* Whenever user encounters a site that uses Cryptic Auth, then just click login. (Even if she doesn't have an account)

Server
------

* Nearly identical to password verification
* Store user's public key liberally in any database

Pseudo server-side auth code:

  login_endpoint(username, message){
    pub_key = get_user_pub_key(username);
    
    if (pub_key == null){
      pub_key = cryptic-auth.get_pub_key(username);
    }
    
    if ( cryptic-auth.verify(username, pub_key, message) ){
      return {"login":"successful"}
    }else{
      return {"login":"incorrect"}
    }  
  }

Gears (how it really works)
---------------------------

Registration:  


A user keeps their public key/private key locally along with a preferred username.

A user first encounters your site and registers by signing the current time with their private key, and sends you the sig, public key, and username

You verify the sig with the public key, and then record the user's public key for verification later.

Login:  

After the first time a user visits the site you should have their public key on record, so you can make sure that it's the same person who registered.






