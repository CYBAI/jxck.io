# [book][indesign] syntax-highlighted tagged text

## Intro

サンプルコードがハイライトされてないのは技術書籍の怠慢


### Javascript


```js
import file from fs

function callback(err, file) {
  if (err) return console.error(err);

  /* ここで色々する */
};

file.open(callback);

class Test extends EventEmitter {
  constructor(data) {
    this.data = data
  }

  jquery() {
    $('body').innerHTML = "alert('xss')"
  }

  promise() {
    return Promise.resolve('foo')
  }
}

const test = new Test()
test.promise().then((e) => {
  console.log(e)
})

export module;
```


### CSS


```css
strong::before,
strong::after {
  content: "**";
}

ul li::before {
  content: "- ";
}

ol {
  counter-reset: list;
}

ol li::before {
  counter-increment: list;
  content: counter(list) ". ";
}

dl dt::after {
  content: ":";
}

blockquote {
  display: block;
  border: solid 1px var(--block-quote);
  border-radius: 4px;
  padding: 0.4em 1em;
  margin: 0;
}
```


### HTML


```html
<!DOCTYPE html>
<meta charset=utf-8>
<meta name=viewport content="width=device-width,initial-scale=1">
<title>DEMO | labs.jxck.io</title>

<style>
</style>

<h1>Test</h1>
<p>this is <strong>sample</strong> text</p>

<div>
  <video src="some.mp4">
  <img src=some.webp label="good picture">

  <form action=/login method=post>
    <input type=text name=username>
    <input type=password name=password>
    <button type=submit>ok</button>
  </form>
</div>

```


### Java


```java
public class DecimalOctal {

    public static void main(String[] args) {
        int decimal = 78;
        int octal = convertDecimalToOctal(decimal);
        System.out.printf("%d in decimal = %d in octal", decimal, octal);
    }

    public static int convertDecimalToOctal(int decimal)
    {
        int octalNumber = 0, i = 1;

        while (decimal != 0)
        {
            octalNumber += (decimal % 8) * i;
            decimal /= 8;
            i *= 10;
        }

        return octalNumber;
    }
}
```


### HTTP


```http
POST /demo/submit/ HTTP/1.1
Host: rouge.jneen.net
Cache-Control: max-age=0
Origin: http://rouge.jayferd.us
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_2) AppleWebKit/535.7 (KHTML, like Gecko) Chrome/16.0.912.63 Safari/535.7
Content-Type: application/json
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Referer: http://pygments.org/
Accept-Encoding: gzip,deflate,sdch
Accept-Language: en-US,en;q=0.8
Accept-Charset: windows-949,utf-8;q=0.7,*;q=0.3

{"name":"test","lang":"text","boring":true}
```


### Go


```go
package main

import (
	"fmt"
	"math"
)

type Abser interface {
	Abs() float64
}

func main() {
	var a Abser
	f := MyFloat(-math.Sqrt2)
	v := Vertex{3, 4}

	a = f  // a MyFloat implements Abser
	a = &v // a *Vertex implements Abser

	// In the following line, v is a Vertex (not *Vertex)
	// and does NOT implement Abser.
	a = v

	fmt.Println(a.Abs())
}

type MyFloat float64

func (f MyFloat) Abs() float64 {
	if f < 0 {
		return float64(-f)
	}
	return float64(f)
}

type Vertex struct {
	X, Y float64
}

func (v *Vertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}
```


### Makefile


```makefile
# Makefile
.PHONY: all
all: main

main: main.o
	gcc -o main main.o

main.o: main.c
	gcc -c main.c

.PHONY: clean
clean:
	rm -rf main main.o
```


### Nginx


```nginx
user       www www;  ## Default: nobody
worker_processes  5;  ## Default: 1
error_log  logs/error.log;
pid        logs/nginx.pid;
worker_rlimit_nofile 8192;

events {
  worker_connections  4096;  ## Default: 1024
}

http {
  include    conf/mime.types;
  include    /etc/nginx/proxy.conf;
  include    /etc/nginx/fastcgi.conf;
  index    index.html index.htm index.php;

  default_type application/octet-stream;
  log_format   main '$remote_addr - $remote_user [$time_local]  $status '
    '"$request" $body_bytes_sent "$http_referer" '
    '"$http_user_agent" "$http_x_forwarded_for"';
  access_log   logs/access.log  main;
  sendfile     on;
  tcp_nopush   on;
  server_names_hash_bucket_size 128; # this seems to be required for some vhosts

  server { # php/fastcgi
    listen       80;
    server_name  domain1.com www.domain1.com;
    access_log   logs/domain1.access.log  main;
    root         html;

    location ~ \.php$ {
      fastcgi_pass   127.0.0.1:1025;
    }
  }

  server { # simple reverse-proxy
    listen       80;
    server_name  domain2.com www.domain2.com;
    access_log   logs/domain2.access.log  main;

    # serve static files
    location ~ ^/(images|javascript|js|css|flash|media|static)/  {
      root    /var/www/virtual/big.server.com/htdocs;
      expires 30d;
    }

    # pass requests for dynamic content to rails/turbogears/zope, et al
    location / {
      proxy_pass      http://127.0.0.1:8080;
    }
  }

  upstream big_server_com {
    server 127.0.0.3:8000 weight=5;
    server 127.0.0.3:8001 weight=5;
    server 192.168.0.1:8000;
    server 192.168.0.1:8001;
  }

  server { # simple load balancing
    listen          80;
    server_name     big.server.com;
    access_log      logs/big.server.access.log main;

    location / {
      proxy_pass      http://big_server_com;
    }
  }
```
