Web-version of Suoma-Sáme-Suoma sátnegirji with PHP and SQLite. This version is under development and will be published during year 2025. The search already works quite well but some additional features are still in progress.

The web app is very lightweight and runs well and fast for example on Raspberry Pii as I do at home.

You'll also need the latest <a href="https://github.com/guovza/satnegirji.db">satnegirji.db</a> SQLite database. Put it somewhere outside your web ducument root. Webserver process need to have access to it anyway. 

Modify the $db variable to suite your configuration:

<pre>
<code>
// Connect to SQLite database
$db = new SQLite3('/var/www/db/satnegirji.db');
</code>
</pre>

I'll suggest you to make sure your webserver is configured properly and securely. Also modify your webserver to run *.html files as PHP files or rename index.html file as index.php file.

I'll also suggest you to make sure your webserver sends some additional security related http headers (CSP). With Apache, you may put the below to your Apache configuration (modify the domain skuolfi.org to suite your own domain.

<pre>
<code>
<IfModule headers_module>
Header always set Strict-Transport-Security: "max-age=63072000; includeSubDomains; preload"
Header always set X-Content-Type-Options: "nosniff"
Header always set X-Frame-Options: "DENY"
header always set Cross-Origin-Resource-Policy: "default-src 'self';"
Header always set Content-Security-Policy: "default-src 'self'; script-src 'self'; connect-src 'self';style-src 'self';base-uri 'self' https://satnegirji.skuolfi.org;frame-src 'self';frame-ancestors 'self';form-action 'self';upgrade-insecure-requests;img-src 'self' data:"
Header always set Referrer-Policy: same-origin
</IfModule>
</code>
</pre>

I'll also suggest you to force https connection. With Apache web-server, you can put this to your conficuration (modify to suite your server):

<pre>
<code>
Redirect permanent / https://your.dictionary.server/
</code>
</pre>

Modify the security.txt as needeed and place it on https://your.dictionary.server/.well-known/security.txt
