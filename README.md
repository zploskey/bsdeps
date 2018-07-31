Test of bsb building a dependency that re-exports a module from an indirect dependency.
Pkga depends on Pkgb which depends on Pkgc.
Pkgb re-exports the Pkgc module as C.
Pkga calls Pkgb.C.hello.

```sh
cd pkgb
npm install
cd ../pkga
npm install
npm run build
```

Produces this build error:
```
> pkga@0.1.0 build /home/zach/src/bsdeps/pkga
> bsb -make-world

Duplicated package: bs-platform /home/zach/src/bsdeps/pkga/node_modules/bs-platform (chosen) vs /home/zach/src/bsdeps/pkga/node_modules/pkgb/node_modules/pkgc/node_modules/bs-platform in /home/zach/src/bsdeps/pkga/node_modules/pkgb/node_modules/pkgc 
[2/2] Building src/pkgc.mlast.d
[1/1] Building src/pkgc.cmj
Duplicated package: bs-platform /home/zach/src/bsdeps/pkga/node_modules/bs-platform (chosen) vs /home/zach/src/bsdeps/pkga/node_modules/pkgb/node_modules/bs-platform in /home/zach/src/bsdeps/pkga/node_modules/pkgb 
[2/2] Building src/pkgb.mlast.d
[1/1] Building src/pkgb.cmj
[2/2] Building src/demo.mlast.d
[1/1] Building src/demo.cmj
File "/home/zach/src/bsdeps/pkga/src/demo.ml", line 1, characters 17-29:
Error: Unbound value Pkgb.C.hello
npm ERR! code ELIFECYCLE
npm ERR! errno 2
npm ERR! pkga@0.1.0 build: `bsb -make-world`
npm ERR! Exit status 2
npm ERR! 
npm ERR! Failed at the pkga@0.1.0 build script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/zach/.npm/_logs/2018-07-31T16_43_55_123Z-debug.log
```

