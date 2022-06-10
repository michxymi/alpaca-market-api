cmake_minimum_required(VERSION 3.14...3.23)

project(
	AlpacaMarket
	VERSION 0.0.1
	DESCRIPTION "A C++ library for the Alpaca Market API"
	LANGUAGES CXX
)

if(CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)

	set(CMAKE_CXX_EXTENSIONS OFF)

	set_property(GLOBAL PROPERTY USE_FOLDERS ON)

	include(CTest)
endif()

include(FetchContent)

FetchContent_Declare(
	nlohmann
	GIT_REPOSITORY https://github.com/nlohmann/json.git
	GIT_TAG v3.10.5
)
FetchContent_MakeAvailable(nlohmann)

add_subdirectory(src)

if((CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME OR ALPACA_MARKET_BUILD_TESTING)
   AND BUILD_TESTING)
  add_subdirectory(tests)
endif()
