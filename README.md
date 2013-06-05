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
- [another cap_sasl.pl script](https://github.com/atheme/atheme/blob/master/contrib/cap_sasl.pl) with DH-AES.  hmmmm

Configuring cap_sasl.pl

> cap_sasl should already be in the repo and configured
> after the irssi conf is linked (shown above) -
> but if not, here's the process:

1. Installing dependencies from [CPAN](http://www.cpan.org/modules/INSTALL.html)
  - I used pivotal-sprout, but my OSX 10.8 has perl 5.12.4.
  - Go [here](http://blog.jambura.com/2013/02/19/setup-homebrew-perlbrew-ruby-rvm-perl-cpanm-nginx-in-mountain-lion/) for issues installing perl.
  - `brew install cpanminus` - Install cpanm
  - `cpanm Crypt::Blowfish Crypt::DH Crypt::OpenSSL::Bignum Math::BigInt Math::BigInt::FastCalc Math::BigInt::GMP` - Install required crypto modules
  - `cpanm` may need `sudo` on OSX.
1. Linking cap_sasl.pl:
  - `cd $HOME/.irssi/scripts`
  - `wget http://www.freenode.net/sasl/cap_sasl.pl`
  - `cd autorun`
  - `ln -sv ../cap_sasl.pl`

## ident.d config
