Web-version of Suoma-Sáme-Suoma sátnegirji with PHP and SQLite.

You'll also need the latest <a href="https://github.com/guovza/satnegirji.db">satnegirji.db</a> SQLite database. Put it somewhere outside your web ducument root. Webserver process need to have access to it anyway. 

Modify the $db variable to suite your configuration:

<pre>
<code>
// Connect to SQLite database
$db = new SQLite3('/var/www/db/satnegirji.db');
</code>
</pre>

I'll suggest you to make sure your webserver is configured properly and securely. I'll also suggest you to make sure your webserver sends some additional security related http headers. With Apache, you may put the below to your Apache configuration (modify the domain skuolfi.org to suite your own domain):

<pre>
<code>
<IfModule headers_module>
Header always set Strict-Transport-Security: "max-age=63072000; includeSubDomains; preload"
Header always set X-Content-Type-Options: "nosniff"
Header always set X-Frame-Options: "DENY"
header always set Cross-Origin-Resource-Policy: same-origin
header always set Content-Security-Policy: "default-src 'self'; img-src 'self' skuolfi.org *.skuolfi.org; style-src 'self'"
Header always set Content-Security-Policy "frame-ancestors 'self';"
Header always set Referrer-Policy: origin-when-cross-origin
</IfModule>
</code>
</pre>

I'll also suggest you to force https connection. With Apache web-server, you can put this to your conficuration (modify to suite your server):

<pre>
<code>
Redirect permanent / https://your.dictionary.server/
</code>
</pre>
