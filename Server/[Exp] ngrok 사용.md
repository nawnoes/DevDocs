# ngrok 사용
ngrok이란 로컬 서버를 임의의 url을 통해 인터넷에 노출시켜주는 역할을 한다. 
NAT와 방화벽 뒤에 있는 로컬서버를 안전한 터널을 통해 공개 인터넷에 노출 시켜 주는 도구
> 포트포워딩과 같은 네트워크 환경설정 변경 없이 로컬에 실행중인 서버를 안전하게 외부에서 접근 가능하게 하는 도구

## 1. 설치
```bash
$ npm i -g ngrok
``` 

## 2. 사용
ngrok http [PORT 번호] 명령을 통해 사용.
```
$ ngrok http 8080

ngrok by @inconshreveable                                                                                    
                        (Ctrl+C to quit)
  
  Session Status                online
  Session Expires               7 hours, 59 minutes
  Version                       2.2.8
  Region                        United States (us)
  Web Interface                 http://127.0.0.1:4040
  Forwarding                    http://7e78ace7.ngrok.io -> localhost:8080
  Forwarding                    https://7e78ace7.ngrok.io -> localhost:8080
  
  Connections                   ttl     opn     rt1     rt5     p50     p90
                                0       0       0.00    0.00    0.00    0.00
```
> 세션 만료는 공식 사이트에서 가입후 진행가능


## 3. 사용 방법
```bash
$ ngrok --help

NAME:
   ngrok - tunnel local ports to public URLs and inspect traffic

DESCRIPTION:
    ngrok exposes local networked services behinds NATs and firewalls to the
    public internet over a secure tunnel. Share local websites, build/test
    webhook consumers and self-host personal services.
    Detailed help for each command is available with 'ngrok help <command>'.
    Open http://localhost:4040 for ngrok's web interface to inspect traffic.

EXAMPLES:
    ngrok http 80                    # secure public URL for port 80 web server
    ngrok http -subdomain=baz 8080   # port 8080 available at baz.ngrok.io
    ngrok http foo.dev:80            # tunnel to host:port instead of localhost
    ngrok tcp 22                     # tunnel arbitrary TCP traffic to port 22
    ngrok tls -hostname=foo.com 443  # TLS traffic for foo.com to port 443
    ngrok start foo bar baz          # start tunnels from the configuration file

VERSION:
   2.2.8

AUTHOR:
  inconshreveable - <alan@ngrok.com>

COMMANDS:
   authtoken	save authtoken to configuration file
   credits	prints author and licensing information
   http		start an HTTP tunnel
   start	start tunnels by name from the configuration file
   tcp		start a TCP tunnel
   tls		start a TLS tunnel
   update	update ngrok to the latest version
   version	print the version string
   help		Shows a list of commands or help for one command
```