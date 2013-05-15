cryptic-auth
============

Simple, and Dev friendly public/private key authentication for the web (and anything else)

* Client has Chrome Plugin or Firefox Add-On installed (Open Source)
* Server implements Library that facilitates Pub/Private Transaction for Auth (Open Source)



Problem
=======

There are too many applications that require a user/pass combination. With so many passwords it's natural to reuse a couple.

Solutions?
----------

OAuth?

* It works, but it is a huge pain to setup; which, unfortunately, hinders it's widespread use.
* Client still needs to login with OAuth Provider

Pub/Priv?

* If it can be packaged well it would be cinch to setup. 
* Client never sends a password! One click login!

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

When a user creates a public key a copy is sent to auth.cryptic.io.

Then whenever a user first encounters your site, you fetch their pub-key from cryptic.

If they are returning you should already have the pub_key stored, if not feel free to get it again from cryptic.

With the pub-key you will decrypt the message sent from the user. 

The message is simply the user's username encrypted with his private-key.

By successfully decrypting the message you verified the user is indeed who they say they are.






