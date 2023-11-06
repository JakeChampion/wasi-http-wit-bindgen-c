# wit-bindgen c potential bug

## Steps to reproduce

### 1 - Use the latest wit-bindgen, which as of today is:
```shell
❯ wit-bindgen --version
```

```shell
wit-bindgen-cli 0.13.1 (880bfabc0 2023-10-30)
```


### 2 - Generate the c-bindings based on the wit definitions:
```shell
❯ wit-bindgen c --no-helpers  --world test-wasi-http . --out-dir out
```

```shell
Generating "out/test_wasi_http.c"
Generating "out/test_wasi_http.h"
Generating "out/test_wasi_http_component_type.o"
```

### 3 - Compile the c-bindings:
```shell
❯ /opt/wasi-sdk/bin/clang out/test_wasi_http.c
```
```shell
In file included from out/test_wasi_http.c:2:
out/test_wasi_http.h:318:9: error: unknown type name 'test_wasi_http_own_request_options_t'; did you mean 'test_wasi_http_borrow_request_options_t'?
typedef test_wasi_http_own_request_options_t test_wasi_http_own_request_options_t;
        ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        test_wasi_http_borrow_request_options_t
out/test_wasi_http.h:244:3: note: 'test_wasi_http_borrow_request_options_t' declared here
} test_wasi_http_borrow_request_options_t;
  ^
1 error generated.
```