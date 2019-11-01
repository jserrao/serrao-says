# Chrome Certificate Error: NET::ERR_CERT_INVALID

If you build enough sites and do dev locally, you'll eventually have a local server that uses TLS to produce it's own HTTPS transactions. 

In this particular example, I've run into issues using [Lando](https://github.com/lando/lando) (thin layer on top of Docker) to stand up a couple of legacy WordPress sites I maintain.

Here's what the error looks like:

[image]

## Localhost gets no love

The error itself deals with 

## Secret passageway...

You can get around this error by performing some black magic. 

> Make sure your browser is focused on the blocked tab. Click anywhere on the screen and type `thisisunsafe` on your keyboard.

Presto, page load. Whoa. First time I saw this, I got up from my desk and walked away, like my computer just did a mic drop on me. But yes, this works. Not a long term solution but maybe you've got a deadline staring at you or it's 4:52p on Friday.

## Really fixing this problem

