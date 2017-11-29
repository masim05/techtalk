# Techtalk

## Build
```
git clone git@github.com:masim05/techtalk.git
cd techtalk
PROJECT_ROOT=`pwd`
git submodule init
git submodule update
cd $PROJECT_ROOT/src/nginx
./auto/configure \
    --prefix=$PROJECT_ROOT/build \
    --add-module=../nginx-push-stream-module \
    --with-http_auth_request_module \
    --builddir=$PROJECT_ROOT/build/objs
make -j4
make install
cd $PROJECT_ROOT/build/sbin/
./nginx -c $PROJECT_ROOT/conf/nginx.conf
```

## Play

### proxy_pass locations
```
curl localhost:8090/endpoint/moved/from/gt ; echo # exact match
curl localhost:8090/pic.jpg                ; echo # regex match
curl localhost:8090/pic.jpgAAA             ; echo # default
curl localhost:8090                        ; echo # default

```

### auth_request
```
curl -H 'AUTH-ME: YES' localhost:8091 ; echo
curl                   localhost:8091 ; echo
```

### load balancing
```
curl localhost:8092/abc ; echo
curl localhost:8092/abc ; echo
curl localhost:8092/abc ; echo
```

### stream from server
```
curl -s -v --no-buffer 'http://localhost:8093/sub/my_channel_1'; echo
curl -s -v -X POST     'http://localhost:8093/pub?id=my_channel_1' -d 'Hello World!'
```