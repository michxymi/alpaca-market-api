FetchContent_Declare(
	googleTest
	GIT_REPOSITORY https://github.com/google/googletest.git
	GIT_TAG release-1.11.0)
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googleTest)

set(${PROJECT_NAME}_TESTS
	BarTests.cpp
	QuoteTests.cpp
	TradeTests.cpp
)

foreach(TEST ${${PROJECT_NAME}_TESTS})

	string(REGEX REPLACE ".cpp" "" title ${TEST})

	add_executable(${title} ${TEST})
	target_compile_features(${title} PRIVATE cxx_std_17)

	target_link_libraries(${title} PRIVATE gtest gtest_main)

	add_test(NAME ${title} COMMAND ${title})

endforeach(TEST ${PROJECT_NAME}_TESTS)
