cmake_minimum_required(VERSION 3.11.0)

cmake_policy(SET CMP0003 NEW)

# https://cmake.org/cmake/help/v3.0/policy/CMP0025.html
# AppleClang
if(POLICY CMP0025)
  cmake_policy(SET CMP0025 NEW)
endif()

# https://cmake.org/cmake/help/v3.6/policy/CMP0026.html
# Disallow LOCATION property
if(POLICY CMP0026)
  cmake_policy(SET CMP0026 NEW)
endif()

# https://cmake.org/cmake/help/v3.0/policy/CMP0042.html
# MACOSX_RPATH is enabled by default
if(POLICY CMP0042)
  cmake_policy(SET CMP0042 NEW)
endif()

project(PVRG)

set(PVRG_SRCS
  jpeg.c
  codec.c
  huffman.c
  io.c
  chendct.c
  leedct.c
  marker.c
  stream.c
  transform.c
  lexer.c)

if(MSVC)
  add_definitions(-DNOTRUNCATE)
else()
  add_definitions(-DSYSV -DNOTRUNCATE)
endif()

#add_definitions(-DIO_DEBUG)
#add_library(pvrg ${PVRG_SRCS})

add_executable(pvrg ${PVRG_SRCS})
#target_link_libraries(pvrgjpeg pvrg)


# Should you wish to modify the interpreter
# modify this portion here.
#
# Make sure that you move the first comment from the start to
# within the braces %{ /* */ %} in lexer.l,
# otherwise it will give you a error (definitions too long).
#
#  Caution: Sometimes -ll is required.
#
#
#lexer.c: lexer.l
#	lex lexer.l
#	mv lex.yy.c lexer.c
#
