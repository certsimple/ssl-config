# SSL Config

A node.js implementation of the recommended cipher suites and TLS/SSL versions from Mozilla's [Server Side TLS](https://github.com/mozilla/server-side-tls) project.

Note **this package only sets cipher suites and TLS/SSL versions**, other parts of the recommendations are implemented elsewhere, eg, for Express servers HSTS we recommend using [Helmet](https://www.npmjs.com/package/helmet).

## Usage

Just use either 'modern', 'intermediate' or 'old'.

### modern

Firefox 27, Chrome 22, IE 11, Opera 14, Safari 7, Android 4.4, Java 8 and newer.

### intermediate

Firefox 1, Chrome 1, IE 7, Opera 5, Safari 1, Windows XP IE8, Android 2.3, Java 7 and newer.

### old

Windows XP IE6, Java 6 and newer. You really shouldn't use this setting, it is implemented for completeness.

Eg:

	var sslConfig = require('ssl-cipher-suites')('high');

Then run `https.createServer` per [node.js TLS](https://nodejs.org/api/tls.html) and [io.js TLS](https://iojs.org/api/tls.html#tls_tls_createserver_options_secureconnectionlistener) docs.

	https.createServer({
		key: privateKey,
		cert: certificate,
		ca: certificateAuthority,
		ciphers: sslConfig.ciphers,
		secureOptions: sslConfig.secureOptions
	});

Or for express.js

	var server = https.createServer({
		key: privateKey,
		cert: certificate,
		ca: certificateAuthority,
		ciphers: sslConfig.ciphers,
		secureOptions: sslConfig.secureOptions
	}, app);

