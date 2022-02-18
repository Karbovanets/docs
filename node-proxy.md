
# How to run Karbo node behind reverse proxy

Here you will learn how to run Karbo node behing the reverse proxy for access in a browser via `https://` protocol, so it can be used as an API for various services, like client-side web wallet, explorer, etc.

We will use nginx for this setup, which is probably the most popular solution. This example is for a VPS server on an Ubuntu. 

You will need a domain and a SSL certificate, you can use a free certificate from Letsencrypt and Cerfbot. We will omit the instructions on how to get certificates and assume you have them.

## Run Karbo daemon

Provided you have a VPS server, run Karbo daemon to let it sync while you set up the proxy.

Here's the example how to run Karbo daemon for a public node:
```
./karbowanecd -i --enable-cors=* --restricted-rpc --rpc-bind-ip 0.0.0.0 --rpc-bind-port 32348 --fee-address=KedFK1bvF665GgTe8HA5dZDLeM4wFEUPzeRS5obaK6dTa12tzjyJeWGPbyX938Xw4zU4XypcSEXtb5BZazBsNj7HS2XZLEp --fee-amount 0.01
```
By these startup flags, you tell daemon to enable CORS headers, enable additional blockchain data for an explorer, restrict some RPC functions, like disable mining so no one can mine on your server. Also, you can set a fee amount and address so you can receive some fees if someone uses your node to work with wallet. Don't expect to get rich though.

Now let's move on to proxy setup.

## Install Nginx

```
sudo apt-get update
sudo apt-get install nginx
```

## Edit the Configuration

Next you will need to edit the default Nginx configuration file.

```
sudo nano /etc/nginx/sites-enabled/default
```

Here is what the final config might look like. You can update or replace the existing config file, although you may want to make a quick copy first.
```
server {
	listen 80 default_server;
	listen [::]:80 default_server;

	root /var/www/html;

	# Add index.php to the list if you are using PHP
	index index.html index.htm index.nginx-debian.html;

	server_name _;

	location / {
		# First attempt to serve request as file, then
		# as directory, then fall back to displaying a 404.
		try_files $uri $uri/ =404;
	}
}

server {
    listen 32448;
    server_name node.karbo.org;

    ssl_certificate           /etc/nginx/cert.crt;
    ssl_certificate_key       /etc/nginx/cert.key;

    ssl on;
    ssl_session_cache  builtin:1000  shared:SSL:10m;
    ssl_protocols  TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers HIGH:!aNULL:!eNULL:!EXPORT:!CAMELLIA:!DES:!MD5:!PSK:!RC4;
    ssl_prefer_server_ciphers on;

    access_log            /var/log/nginx/node.karbo.org.log;

    location / {

      proxy_set_header        Host $host;
      proxy_set_header        X-Real-IP $remote_addr;
      proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header        X-Forwarded-Proto $scheme;

      proxy_pass          http://0.0.0.0:32348;
      proxy_read_timeout  90;
    }
}
```

Start nginx:
```
systemctl start nginx
```

If you followed the instructions and have done all correctly, your node now will be accessible via `http://` protocol at its default port 32348 like this http://node.karbo.org:32348/ and via `https://` protocol at 32448 port, like this https://node.karbo.org:32448/.

This setup is not meant for native wallets to work with node via https:// protocol, point them to 32348 port via http:// instead.