set(HDR_DIR ../include/alpaca)
set(${PROJECT_NAME}_HDRS
	${HDR_DIR}/Bar.hpp
	${HDR_DIR}/Quote.hpp
	${HDR_DIR}/ResponseObject.hpp
	${HDR_DIR}/Trade.hpp

)

set(${PROJECT_NAME}_SRCS
	Bar.cpp
	Quote.cpp
	Trade.cpp
)

add_library(${PROJECT_NAME} SHARED
	${${PROJECT_NAME}_HDRS}
	${${PROJECT_NAME}_SRCS}
)

target_include_directories(${PROJECT_NAME} 
	PUBLIC
		$<INSTALL_INTERFACE:include>
		$<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
	PRIVATE
		${nlohmann_SOURCE_DIR}/single_include

)

target_compile_features(${PROJECT_NAME} PUBLIC cxx_std_17)

set_target_properties(${PROJECT_NAME} PROPERTIES
	ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
	LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
	RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
	OUTPUT_NAME ${PROJECT_NAME}
	VERSION ${PROJECT_VERSION}
	SOVERSION ${PROJECT_VERSION_MAJOR}
)

if(WIN32)
	set_target_properties(${PROJECT_NAME} PROPERTIES WINDOWS_EXPORT_ALL_SYMBOLS TRUE)
	set_target_properties(${PROJECT_NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")
endif(WIN32)

export(TARGETS ${PROJECT_NAME} FILE ${PROJECT_NAME}Config.cmake)