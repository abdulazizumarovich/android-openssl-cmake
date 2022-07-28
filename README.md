# OpenSSL For Android 

* Include `build-openssl.sh` in your app (Preferrably in the app's root folder)
* Run it once
* This will make a folder `prefix` which will have OpenSSL libraries

## Using in cmake

Add these to your `CMakeLists.txt` app :

```
set(OPENSSL_ROOT_DIR path-to-prefix-folder)
set(OPENSSL_INCLUDE_DIR ${OPENSSL_ROOT_DIR}/include)
set(OPENSSL_CRYPTO_LIBRARY ${OPENSSL_ROOT_DIR}/lib/libcrypto.a)

set(OPENSSL_USE_STATIC_LIBS TRUE)
find_package(OpenSSL REQUIRED)
message("OpenSSL dir: ${OPENSSL_ROOT_DIR}")

if(OPENSSL_FOUND)
    message("OpenSSL ver: ${OPENSSL_VERSION}")
else()
    message("OpenSSL not found")
endif()

target_link_libraries(UnifiedLib OpenSSL::Crypto)
```

If your CMake file is at `app/src/main/cpp/CMakeLists.txt` and the `prefix` folder is in app root then it will be :

```
set(OPENSSL_ROOT_DIR ${CMAKE_CURRENT_LIST_DIR}/../../../../prefix/${CMAKE_ANDROID_ARCH_ABI})
```

This is used in [Dots app](https://github.com/subins2000/Dots)
