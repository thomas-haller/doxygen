find_package(Iconv)

include_directories(
	${CMAKE_SOURCE_DIR}/src
	${GENERATED_SRC}
	${CMAKE_SOURCE_DIR}/qtools
	${ICONV_INCLUDE_DIR}
	${CLANG_INCLUDEDIR}
)

add_executable(doxyparse
doxyparse.cpp
)

if (use_libclang)
    set(CLANG_LIBS libclang clangTooling ${llvm_libs})
endif()

target_link_libraries(doxyparse
_doxygen
qtools
md5
doxycfg
vhdlparser
${ICONV_LIBRARIES}
${CMAKE_THREAD_LIBS_INIT}
${SQLITE3_LIBRARIES}
${EXTRA_LIBS}
${CLANG_LIBS}
)

install(TARGETS doxyparse DESTINATION bin)
