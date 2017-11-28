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