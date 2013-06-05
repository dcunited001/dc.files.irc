dc.files.irc
============

includes:
* identd.user => /usr/local/etc/identd.user
* irssi config: irssi/config => ~/.irssi/config

installed identd via brew from: [https://github.com/alexbarton/homebrew-alex/blob/master/identd.rb](alexbarton/homebrew-alex)

> identd provides "authentication" for IRC and is easily spoofed.  the main reason it exists is to .. well nevermind.

## irssi config

#### ~/.irssi/config

Linking irssi configuration:

- `mkdir ~/.irssi`
- `cd !$`
- `lns $DF/irc/irssi/config config`
- `lns $DF/irc/scripts scripts`

#### irssi plugins

#### Authentication with SASL

- [cap_sasl.pl script](http://www.freenode.net/sasl/cap_sasl.pl)
- [irssi & SASL install guide](http://www.andrews-corner.org/irssi.html)
- [another irssi & SASL install guide](http://blog.freenode.net/2010/01/connecting-to-freenode-using-tor-sasl/)

Configuring cap_sasl.pl

> cap_sasl should already be in the repo and configured
> after the irssi conf is linked (shown above) -
> but if not, here's the process:

- `cd $HOME/.irssi/scripts`
- `wget http://www.freenode.net/sasl/cap_sasl.pl`
- `cd autorun`
- `ln -sv ../cap_sasl.pl`

## ident.d config
