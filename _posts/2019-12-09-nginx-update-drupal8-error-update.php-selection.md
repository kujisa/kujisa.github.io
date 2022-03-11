---
layout: post
title: nginx下drupal 8升级update.php selection 错误
author: Kujisa
categories: Other
tags: Drupal Nginx
---

在drupal 8 伪静态文件中添加几行代码。
伪静态文件默认地址`/usr/local/nginx/conf/rewrite/drupal.conf`

完整的rewrite代码如下：

{% highlight bash linenos %}
if (!-e $request_filename) {
  rewrite ^/update.php(.*)$ /update.php?q=$1 last;
  rewrite ^/(.*)$ /index.php?q=$1 last;
}

 
location ~ ^/(index|update)\.php(/|$) {
fastcgi_pass unix:/dev/shm/php-cgi.sock;
fastcgi_split_path_info ^(.+\.php)(/.*)$;
 
include fastcgi_params;
fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
fastcgi_param DOCUMENT_ROOT $realpath_root;
fastcgi_intercept_errors on;
}
{% endhighlight %}

保存后，停止并重新启动nginx服务，顺利升级。

1. 查看nginx进程号
`ps -ef|grep nginx`
2. 终止进程
`kill -quit 进程号`
3. 如果页面无法访问，重启服务器就好
`reboot`