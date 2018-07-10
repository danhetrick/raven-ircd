![Raven IRCd](https://github.com/danhetrick/raven-ircd/blob/master/raven_ircd.png?raw=true)

# Raven IRCd

Raven IRCd (or rIRCd) is an IRC server written in Perl, with POE.  It is still very much a work in progress, but its base functionality is complete.  Clients can connect to it, join channels, and do all the things that other IRCds can do.

# Usage

	perl rircd.pl <CONFIGURATION FILE>

By default, Raven IRCd will load a file named `ircd.xml` located either in the directory where `rircd.pl` is located, or in the `config/` directory, in the same directory as `rircd.pl`.  The directory where `rircd.pl` is located will be called the **home directory** in the rest of this document;  the `/config` directory located in the home directory will be called the **config directory**.

# Configuration

Raven IRCd configuration files are written in XML, and have several useful features.

## `import` element

The `import` element is used to load configuration data from external files, much like C's `#include` preprocesser directive.  Raven IRCd will look for `import`'ed files first in the home directory, then in the config directory.  The `import` element has no children elements.

## `config` element

The `config` element is where all the main server settings are.  They are all optional; the server will use a listening port of `6667` and let anyone connect to it.  `config` has a number of children elements.  Here's an example of a basic `config` entry, with all default settings:

	<?xml version="1.0" encoding="UTF-8"?>
	<config>

		<verbose>1</verbose>
		<port>6667</port>
		<name>Perl.IRC.Server</name>
		<nicklength>15</nicklength>
		<network>PerlNet</network>

		<max_targets>4</max_targets>
		<max_channels>15</max_channels>
		<info>My IRC Server</info>

	</config>

### `verbose`

Set this element to 1 if you want to turn on verbosity;  set it to 0 to turn it off.  If `verbose` is turned on, various data will be printed to the console during runtime.

### `port`

Sets the port that Raven IRCd will listen on.  Multiple `port` elements can exist; each one will spawn a listener on the given port.

### `name`

Sets the server's name.

### `nicklength`

Sets the maximum number of characters that can be used in a client's nick.