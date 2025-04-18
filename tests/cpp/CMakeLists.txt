##
## CMake build script for the yaramod tests.
##

# Source files.
set(SOURCES
	clone_tests.cpp
	tokenstream_tests.cpp
	representation_tests.cpp
	builder_tests.cpp
	parser_tests.cpp
	trie_tests.cpp
	utils_tests.cpp
	visitor_tests.cpp
	yara_file_tests.cpp
	yaramod_tests.cpp
)

if(NOT TARGET yaramod_tests)
	# Executable.
	add_executable(yaramod_tests ${SOURCES})

	# Linking.
	target_link_libraries(yaramod_tests yaramod gtest gtest_main)

	# Includes.
	target_include_directories(yaramod_tests PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}")

	if(YARAMOD_ASAN)
		target_compile_options(yaramod_tests PRIVATE "-fsanitize=address" "-fno-omit-frame-pointer")
		target_link_options(yaramod_tests PRIVATE "-fsanitize=address")
	endif()
endif()
