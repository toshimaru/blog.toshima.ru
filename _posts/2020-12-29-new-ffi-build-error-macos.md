---
layout: post
title: ffi ffi_prep_closure BuildError on macOS
tags: mac gem
---

## Issue

I encountered `ffi` gem build error while running `bundle install`

```
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    current directory: /Users/toshimaru/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/ffi-1.14.2/ext/ffi_c
/Users/toshimaru/.rbenv/versions/2.7.1/bin/ruby -I /Users/toshimaru/.rbenv/versions/2.7.1/lib/ruby/2.7.0 -r
./siteconf20201228-73606-f28m46.rb extconf.rb
checking for ffi_prep_closure_loc() in -lffi... yes
checking for ffi_prep_cif_var()... yes
checking for ffi_raw_call()... yes
checking for ffi_prep_raw_closure()... yes
creating extconf.h
creating Makefile

current directory: /Users/toshimaru/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/ffi-1.14.2/ext/ffi_c
make "DESTDIR=" clean

current directory: /Users/toshimaru/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/ffi-1.14.2/ext/ffi_c
make "DESTDIR="
compiling AbstractMemory.c
compiling ArrayType.c
compiling Buffer.c
compiling Call.c
compiling ClosurePool.c
compiling DynamicLibrary.c
compiling Function.c
Function.c:847:17: error: implicit declaration of function 'ffi_prep_closure_loc' is invalid in C99
[-Werror,-Wimplicit-function-declaration]
    ffiStatus = ffi_prep_closure_loc(closure->pcl, &fnInfo->ffi_cif, callback_invoke, closure, code);
                ^
Function.c:847:17: note: did you mean 'ffi_prep_closure'?
/Library/Developer/CommandLineTools/SDKs/MacOSX10.14.sdk/usr/include/ffi/ffi.h:269:1: note: 'ffi_prep_closure' declared here
ffi_prep_closure(
^
1 error generated.
make: *** [Function.o] Error 1

make failed, exit code 2

Gem files will remain installed in /Users/toshimaru/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/ffi-1.14.2 for
inspection.
Results logged to
/Users/toshimaru/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/extensions/x86_64-darwin-18/2.7.0/ffi-1.14.2/gem_make.out

An error occurred while installing ffi (1.14.2), and Bundler cannot continue.
Make sure that `gem install ffi -v '1.14.2' --source 'https://rubygems.org/'` succeeds before bundling.

In Gemfile:
  bootstrap-sass was resolved to 3.4.1, which depends on
    sassc was resolved to 2.4.0, which depends on
      ffi
```

## Solution

Install `ffi` with opttion `--disable-system-libffi`.

```console
$ gem install ffi -- --disable-system-libffi
```

```console
# x.x.x is version
$ gem install ffi:x.x.x -- --disable-system-libffi
```

## References

- [dyld: Symbol not found: _ffi_prep_closure_loc on Macos 10.14 · Issue #791 · ffi/ffi](https://github.com/ffi/ffi/issues/791)
- [Missing ffi_prep_closure for ffi-1.13.1 gem \| by Jialiang Liang \| Medium](https://medium.com/@leoliang.climber/missing-ffi-prep-closure-error-for-ffi-1-13-1-gem-70f800a48090)
