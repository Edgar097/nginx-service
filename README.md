# nginx-service
nginx script for running nginx service in ( /etc/init.d )


Steps:

	1. sudo apt update
	2. sudo apt install gcc make zlib1g-dev libpcre3-dev libssl-dev wget nano
	3. wget http://nginx.org/download/nginx-1.20.2.tar.gz
	4. tar -xzvf <tar-file>
	5. Look for the configure file => cd <nginx-directory>
	6. ./configure --help  *optional
	7. ./configure --prefix=/etc/nginx \
	--sbin-path=/usr/sbin/nginx \
	--modules-path=/usr/lib/nginx/modules \
	--conf-path=/etc/nginx/nginx.conf \
	--error-log-path=/var/log/nginx/error.log \ 
	--http-log-path=/var/log/nginx/access.log \
	--pid-path=/var/run/nginx.pid \
	--lock-path=/var/run/nginx.lock \
	--http-client-body-temp-path=/var/cache/nginx/client_temp \
	--http-proxy-temp-path=/var/cache/nginx/proxy_temp \
	--http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
	--http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp \
	--http-scgi-temp-path=/var/cache/nginx/scgi_temp \
	--user=nginx \
	--group=nginx \
	--with-compat \
	--with-file-aio \
	--with-threads \
	--with-http_addition_module \
	--with-http_auth_request_module \
	--with-http_dav_module \
	--with-http_flv_module \
	--with-http_gunzip_module \
	--with-http_gzip_static_module \
	--with-http_mp4_module \
	--with-http_random_index_module \
	--with-http_realip_module \
	--with-http_secure_link_module \
	--with-http_slice_module \
	--with-http_ssl_module \
	--with-http_stub_status_module \
	--with-http_sub_module \
	--with-http_v2_module \
	--with-mail \
	--with-mail_ssl_module \
	--with-stream \
	--with-stream_realip_module \
	--with-stream_ssl_module \
	--with-stream_ssl_preread_module \
	--with-cc-opt='-g \
	-O2 \
	-ffile-prefix-map=/data/builder/debuild/nginx-1.21.6/debian/debuild-base/nginx-1.21.6=. \
	-fstack-protector-strong \
	-Wformat \
	-Werror=format-security \
	-Wp,-D_FORTIFY_SOURCE=2 \
	-fPIC' \
	--with-ld-opt='-Wl,-z,relro \
	-Wl,-z,now \
	-Wl,--as-needed \
	-pie' \
	8. Working command 
		○ ./configure  --prefix=/etc/nginx --sbin-path=/usr/sbin/nginx --modules-path=/usr/lib/nginx/modules --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --pid-path=/var/run/nginx.pid --lock-path=/var/run/nginx.lock --http-client-body-temp-path=/var/cache/nginx/client_temp --http-proxy-temp-path=/var/cache/nginx/proxy_temp --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp --http-scgi-temp-path=/var/cache/nginx/scgi_temp --user=nginx --group=nginx --with-compat --with-file-aio --with-threads --with-http_addition_module --with-http_auth_request_module --with-http_dav_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_mp4_module --with-http_random_index_module --with-http_realip_module --with-http_secure_link_module --with-http_slice_module --with-http_ssl_module --with-http_stub_status_module --with-http_sub_module --with-http_v2_module --with-mail --with-mail_ssl_module --with-stream --with-stream_realip_module --with-stream_ssl_module --with-stream_ssl_preread_module --with-cc-opt='-g -O2 -ffile-prefix-map=/data/builder/debuild/nginx-1.21.6/debian/debuild-base/nginx-1.21.6=. -fstack-protector-strong -Wformat -Werror=format-security -Wp,-D_FORTIFY_SOURCE=2 -fPIC' --with-ld-opt='-Wl,-z,relro -Wl,-z,now -Wl,--as-needed -pie'
	9. useradd nginx 
	10. mkdir -p /var/lib/nginx/tmp/ 
	11. chown -R nginx.nginx /var/lib/nginx/tmp/
	12. make
	13. make install
	14. Now u need to setup the nginx service 
		○ Systemd service file -> https://www.nginx.com/resources/wiki/start/topics/examples/systemd/
		○ With the script **nginx** if you are using "service"
    
 	Check the version that you want and copy the url http://nginx.org/en/download.html



Building Dynamic Modules


   	1. Fetch the Nginx Source (same as that of production Nginx version)
	2. Fetch the Module Source
	3. Build Dynamic Module
	4. Reference Module Path within nginx configuration
	
	Steps:
	
	• You need the source file of nginx and the module directory to compile the module
	Ø apt install git
	Ø git clone https://github.com/perusio/nginx-hello-world-module 
	Ø ./configure --add-dynamic-module=/path/module/nginx-hello-world-module (in the source file of nginx, needs to be in the same nginx version)
	Ø make modules
	Ø cd /objs
	Ø Save the module on /etc/nginx/modules/<module> > cp ngx_http_hello_world_module.so /etc/nginx/modules (create de modules directory)
	• Then load the module in the nginx.conf as:
		○ load_module /etc/nginx/modules/<module> Example: load_module /etc/nginx/modules/ngx_hello_world_module.so
		
If you get a binary error, that means the module is not compatible with the nginx version.

Example use: https://github.com/perusio/nginx-hello-world-module
Uses this nginx version http://nginx.org/download/nginx-1.16.1.tar.gz
