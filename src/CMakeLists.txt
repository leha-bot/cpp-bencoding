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
target_include_directories(bencoding PUBLIC
	$<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/../include>
	$<INSTALL_INTERFACE:${INSTALL_INCLUDE_DIR}>
)

# C++11 (or later) is required.
target_compile_features(bencoding PUBLIC cxx_std_11)

install(TARGETS bencoding EXPORT bencoding-config DESTINATION "${INSTALL_LIB_DIR}")
install(EXPORT bencoding-config NAMESPACE bencoding:: DESTINATION "${INSTALL_LIB_DIR}/cmake/bencoding")

