# Sets the minimum version of CMake required to build your native library.
# This ensures that a certain set of CMake features is available to
# your build.

cmake_minimum_required(VERSION 3.4.1)
project(bc-sskr)

# Specifies a library name, specifies whether the library is STATIC or
# SHARED, and provides relative paths to the source code. You can
# define multiple libraries by adding multiple add_library() commands,
# and CMake builds them for you. When you build your app, Gradle
# automatically packages shared libraries with your APK.

# define source files
file(GLOB_RECURSE BC_CRYPTO_BASE "../../deps/bc-crypto-base/src/*.c")

file(GLOB_RECURSE BC_SHAMIR "../../deps/bc-shamir/src/*.c")

file(GLOB_RECURSE BC_SSKR "../../deps/bc-sskr/src/*.c")

# define include dir
include_directories(../../deps/bc-crypto-base/src ../../deps/bc-shamir/src ../../deps/bc-sskr/src /usr/local/include)

# compile
add_library(bc-crypto-base STATIC ${BC_CRYPTO_BASE})

add_library(bc-shamir STATIC ${BC_SHAMIR})

add_library(bc-sskr STATIC ${BC_SSKR})

add_library(jni-utils STATIC ../../base-jni/jni-utils.c)

add_library(bc-sskr-jni SHARED ../java/src/main/jniLibs/sskr-jni.c)

# link
target_link_libraries(bc-shamir bc-crypto-base)

target_link_libraries(bc-sskr bc-shamir)

target_link_libraries(bc-sskr-jni jni-utils)

target_link_libraries(bc-sskr-jni bc-sskr)