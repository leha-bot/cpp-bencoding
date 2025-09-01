##
## Project:   cpp-bencoding
## Copyright: (c) 2014 by Petr Zemek <s3rvac@gmail.com> and contributors
## License:   BSD, see the LICENSE file for more details
##
## CMake configuration file for the library source files.
##

set(BENCODING_SOURCES
	BDictionary.cpp
	BInteger.cpp
	BItem.cpp
	BItemVisitor.cpp
	BList.cpp
	BString.cpp
	Decoder.cpp
	Encoder.cpp
	PrettyPrinter.cpp
	Utils.cpp
)

add_library(bencoding ${BENCODING_SOURCES})

##
## Includes.
##

target_include_directories(bencoding PUBLIC
	$<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/../include>
	$<INSTALL_INTERFACE:${INSTALL_INCLUDE_DIR}>
)

# C++11 (or later) is required.
target_compile_features(bencoding PUBLIC cxx_std_11)

##
## Compiler options.
##

## GCC and Clang specific.

if(CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang")

	# Enable pedantic warnings.
	target_compile_options(bencoding PRIVATE "-pedantic")

	# Abort compilation upon the first error.
	target_compile_options(bencoding PRIVATE "-Wfatal-errors")

	# Standard warning parameters.
	target_compile_options(bencoding PRIVATE -Wall -Wextra)

	# Enable additional warnings that are not included in -Wall and -Wextra
	# (according to `man gcc`).
	target_compile_options(bencoding PRIVATE "-Wcast-align")
	target_compile_options(bencoding PRIVATE "-Wcast-qual")
	target_compile_options(bencoding PRIVATE "-Wfloat-equal")
	target_compile_options(bencoding PRIVATE "-Wold-style-cast")
	target_compile_options(bencoding PRIVATE "-Wswitch-default")
	target_compile_options(bencoding PRIVATE "-Wuninitialized")
endif()

## GCC only flags.

if(CMAKE_CXX_COMPILER_ID MATCHES "GNU")
	target_compile_options(bencoding PRIVATE "-Wuseless-cast")
endif()

##
## Install library and generate package for find_package(bencoding).
##

install(TARGETS bencoding EXPORT bencoding-config DESTINATION "${INSTALL_LIB_DIR}")
install(EXPORT bencoding-config NAMESPACE bencoding:: DESTINATION "${INSTALL_LIB_DIR}/cmake/bencoding")

