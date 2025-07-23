# Packaging tests

These tests check correctness of CMake packaging.
There are currently one test for `find_package(bencoding)`.
For testing, you should: 
1. Build and install cpp-bencoding into some directory ("prefix");
2. Run CMake with additional flag `-Dbencoding_DIR=<prefix>/lib/cmake/bencoding`
3. Try to build and run this test.
4. Test is considered successfull if it has built and run correctly.

