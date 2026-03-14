cmake_minimum_required(VERSION 4.1)

project(sse_mathfun_extension)

add_executable(sse_mathfun_test
    sse_mathfun_test.c)
target_compile_definitions(sse_mathfun_test PUBLIC USE_SSE2 HAVE_SYS_TIMES)
target_link_libraries(sse_mathfun_test m)