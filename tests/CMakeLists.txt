cmake_minimum_required(VERSION 3.16.0)

project(test_antichess_tb_api LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(${PROJECT_NAME}
	test.cpp
)

target_include_directories(${PROJECT_NAME}
	PRIVATE ../src
)

target_compile_definitions(${PROJECT_NAME}
	PRIVATE ANTI
	PRIVATE USE_POPCNT
	PRIVATE USE_PEXT
)

if (WIN32)
	target_link_libraries(${PROJECT_NAME}
		antichess_tb_api
	)
else()
	find_package(Threads REQUIRED)
	target_link_libraries(${PROJECT_NAME}
		antichess_tb_api
		Threads::Threads
		-lstdc++fs
	)
endif()
