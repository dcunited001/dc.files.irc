dc.files.irc
============

includes:
* identd.user => /usr/local/etc/identd.user
* irssi config: irssi/config => ~/.irssi/config

## Irssi Config

- [Official Documentation](http://www.irssi.org/documentation/manual)
- [Config Example](http://misc.nybergh.net/pub/irssi/config.example)
- [Another Config Example](http://carina.org.uk/irssiconfig)
- [IRSSI Config Generator](http://www.matthew.ath.cx/programs/irssiconfig)

#### ~/.irssi/config

Linking irssi configuration:

- `mkdir ~/.irssi`
- `cd !$`
- `lns $DF/irc/irssi/config config`
- `lns $DF/irc/scripts scripts`

Adding an IRC Server:

- `irssi` to open irssi
- `/network add Freenode`
- `/server add -auto -ssl -ssl_verify -network Freenode chat.freenode.net 6667`

#### ~/.irssi/startup

> Put commands into ~/.irssi/startup file, each command on its own line.
> The preceding slash (/) is not necessary.

#### [Irssi Plugins](http://scripts.irssi.org/)

- these are perl scripts downloaded into `$HOME/.irssi/scripts/`
- to autorun a script when irssi starts - `cd $HOME/.irssi/scripts/autorun && ln -sv ../[script].pl`

#### Authentication with SASL

- [cap_sasl.pl script](http://www.freenode.net/sasl/cap_sasl.pl)
- [irssi & SASL config](http://freenode.net/sasl/sasl-irssi.shtml) at Freenode
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
  - `brew install gmp` - resolves dependency for Math::BigInt::GMP
  - `cpanm Crypt::Blowfish Crypt::DH Crypt::OpenSSL::Bignum Math::BigInt Math::BigInt::FastCalc Math::BigInt::GMP` - Install required crypto modules
  - `cpanm` may need `sudo` on OSX.
1. Linking cap_sasl.pl:
  - `cd $HOME/.irssi/scripts`
  - `wget http://www.freenode.net/sasl/cap_sasl.pl`
  - `cd autorun`
  - `ln -sv ../cap_sasl.pl`
1. Configuring SASL Auth
  - Open irssi
  - `/sasl set [network] [user] [pass] [mechanism]`
    - network =~ chat.freenode.net
    - mechanism =~ PLAIN or DH-BLOWFISH (extra config required for DH-AES)
  - `/sasl save` - saves to $HOME/.irssi/sasl.auth - not in source control!

## ident.d config

> not really sure if i'll need ident.d config right now

installed identd via brew from: [https://github.com/alexbarton/homebrew-alex/blob/master/identd.rb](alexbarton/homebrew-alex)

> identd provides "authentication" for IRC and is easily spoofed.  the main reason it exists is to .. well nevermind.
