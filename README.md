# SSL Config

A node.js implementation of the recommended cipher suites and TLS/SSL versions from Mozilla's [Server Side TLS](https://github.com/mozilla/server-side-tls) project.

The suite list uses [the cipher suite prioritization logic from Mozilla](https://wiki.mozilla.org/Security/Server_Side_TLS#Prioritization_logic). Since [Firefox](https://www.ssllabs.com/ssltest/viewClient.html?name=Firefox&version=35&platform=OS%20X) and [Chrome](https://www.ssllabs.com/ssltest/viewClient.html?name=Chrome&version=40&platform=OS%20X) don't support AES-GCM with 256 bit keys, a 128 bit AES key is considered superior.

Note **this package only sets cipher suites and TLS/SSL versions**, other parts of the recommendations are implemented elsewhere, eg, for Express servers HSTS we recommend using [Helmet](https://www.npmjs.com/package/helmet).

## Usage

Just use either 'modern', 'intermediate' or 'old'.

### modern

Requires IE 11, Firefox 27, Chrome 22, Safari 7, Android 4.4, Opera 14, Java 8 or newer.

### intermediate

Requires IE 7, Firefox 1, Chrome 1, Safari 1, Windows XP IE8, Android 2.3, Opera 5, Java 7 or newer.

### old

Windows XP IE6, Java 6 and newer. You really shouldn't use this setting, it is implemented for compatibility with Mozilla's tools.

Eg:

	var sslConfig = require('ssl-config')('modern');

Then run `https.createServer` per [node.js TLS](https://nodejs.org/api/tls.html) and [io.js TLS](https://iojs.org/api/tls.html#tls_tls_createserver_options_secureconnectionlistener) docs.

	https.createServer({
		key: privateKey,
		cert: certificate,
		ca: certificateAuthority,
		ciphers: sslConfig.ciphers,
		honorCipherOrder: true,
		secureOptions: sslConfig.minimumTLSVersion
	});

Or for express.js

	var server = https.createServer({
		key: privateKey,
		cert: certificate,
		ca: certificateAuthority,
		ciphers: sslConfig.ciphers,
		honorCipherOrder: true,
		secureOptions: sslConfig.minimumTLSVersion
	}, app);

Or for [Hapi](http://hapijs.com/):

```
var server = new Hapi.Server();
server.connection({
  // other config options here
  tls: {
    key: privateKey,
    cert: certificate,
    ca: certificateAuthority,
    ciphers: sslConfig.ciphers,
    honorCipherOrder: true,
    secureOptions: sslConfig.minimumTLSVersion
  },
  routes: {
    security: true // turns on HSTS and other security headers
  }
});
```

## License

Mozilla Public License 2.0
