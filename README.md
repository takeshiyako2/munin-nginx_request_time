munin-nginx_request_time
========================

Munin plugin for nginx request time

![munin-nginx_request_time example](https://raw.githubusercontent.com/t-cyrill/munin-nginx_request_time/master/images/example.png "munin-nginx_request_time example")


Modes
----------------

### Default

 * min, median, 90th percentile, 95th percentile

### max

 * max

Usage
----------------

Change nginx log format.
Nginx must be configured to get $request_time.  
nginx_request_time expects LTSV log format.  

```
/etc/nginx/nginx.conf

log_format  ltsv  "time:$time_local"
                  "\thost:$remote_addr"
                  "\tforwardedfor:$http_x_forwarded_for"
                  "\treq:$request"
                  "\tstatus:$status"
                  "\tsize:$body_bytes_sent"
                  "\treferer:$http_referer"
                  "\tua:$http_user_agent"
                  "\treqtime:$request_time"
                  "\tcache:$upstream_http_x_cache"
                  "\truntime:$upstream_http_x_runtime"
                  "\tvhost:$host";

access_log  /var/log/nginx/access.log  ltsv; 
```

Reload Nginx.
```
/etc/init.d/nginx configtest
/etc/init.d/nginx reload
```


munin-nginx_request_time plugin needs Statistics modules.

```
sudo cpanm install Text::LTSV
sudo cpanm install File::ReadBackwards
sudo cpanm install Statistics::Lite
sudo cpanm install Statistics::Descriptive
```

And then,

```
ln -s /usr/share/munin/plugins/nginx_request_time /etc/munin/plugins/nginx_request_time
ln -s /usr/share/munin/plugins/nginx_request_time /etc/munin/plugins/nginx_request_time_max
```

Restart munin-node.
```
service munin-node restart
```

Configration
----------------

### logfile

* ie. /var/log/nginx/access.log

### loglimit

* ie. 1000

### Example

```
[nginx_request_time]
    env.logfile /var/log/nginx/access.log
    env.loglimit 1000
```
