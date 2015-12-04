dc.files.irc
============

includes:
* identd.user => /usr/local/etc/identd.user
* irssi config: irssi/config => ~/.irssi/config

# Weechat

### Weechat Links

- [Weechat FAQ](https://weechat.org/files/doc/weechat_faq.en.html)A
- [Config Guide](/etc/ssl/certs/ca-certificates.crt)

### Weechat Sec Config

Weechat's `sec.conf` should not be stored in the repo.  Use `/secure ...` command to add to weechat's secure config.  These options can be accessed within other `*.conf` files using `"${irc.config.key}"`

### Weechat SSL Config

You'll need the following configuration changes:

```
/set irc.server.freenode.ssl on
/set irc.server.
```

I'm kind of frustrated that I'm expected to use older versions of TLS/SSL & that I'm expected to use `%COMPAT`, *which may allow downgrade attacks.*  All in all though, at least using SSL and SASL makes it quite a bit harder to manipulate traffic.

This reference provides more info on [SSL Priority Strings](http://gnutls.org/manual/html_node/Priority-Strings.html).

```
# This command should not require %COMPAT
# - it allows server client to renegotiate TLS connection details!
/set irc.server.xxx.ssl_priorities "NORMAL:-VERS-TLS-ALL:+VERS-TLS1.0:+VERS-SSL3.0:%COMPAT"

# This is what i'd prefer to use
/set irc.server.xxx.ssl_priorities "NORMAL:-VERS-TLS-ALL:+VERS-TLS1.2:+VERS-TLS1.3"
```

On OSX configuration, you need to download a certificate authority PEM file.  A freely available file is [here](http://curl.haxx.se/docs/caextract.html).  This will need to be added to your system.  The default location is `/etc/ssl/certs/ca-certificates.crt`, but this file does not exist on OSX.  You'll need to add the PEM file you downloaded to your system.

You can choose an alternative location for a PEM file with the following Weechat config command.

```
/set weechat.network.gnutls_ca_file "/etc/ssl/certs/ca-certificates.crt"
```

### Weechat SASL configuration

SASL should be used for additional security.  I'll update this when I've configured it for weechat.

# Irssi


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

#### [Irssi Basics](http://irssi.org/beginner/)

It's like emacs all over again lol

The 2 most important commands:

1. `/help`
1. `/help [command]`

#### [Irssi Keymap](http://irssi.org/beginner/#c9)

Irssi can be configured with any key binding that the terminal forwards to the process.

- M-1 - M-0: `/window goto [1-10]`
- M-q - M-p: `/window goto [11-20]`

#### [Irssi Plugins](http://scripts.irssi.org/)

- these are perl scripts downloaded into `$HOME/.irssi/scripts/`
- to autorun a script when irssi starts - `cd $HOME/.irssi/scripts/autorun && ln -sv ../[script].pl`

#### Authentication with SASL

- [cap_sasl.pl script](http://www.freenode.net/sasl/cap_sasl.pl)
- [irssi & SASL config](http://freenode.net/sasl/sasl-irssi.shtml) at Freenode
- [irssi & SASL install guide](http://www.andrews-corner.org/irssi.html)
- [irssi & SASL on OSX](http://buffered.io/posts/irssi-and-sasl-on-osx)
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
