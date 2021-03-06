cmake_minimum_required(VERSION 3.10)
hunter_add_package(GTest)
find_package(GTest REQUIRED)
find_package(Threads REQUIRED)

add_executable(
    unit_test
    unit_test.cpp
    unit-rest_api.cpp
    unit-dispatch_payload.cpp
    unit-payload.cpp
    unit-gateway.cpp
    unit-user.cpp
    unit_persistent-state.cpp
    ${DISCORDCPP_PRIVATE_HEADERS}
)

target_link_libraries(
    unit_test
    discordcpp
    ${GTEST_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT}
)
target_include_directories(unit_test PRIVATE ${GTEST_INCLUDE_DIRS} ${DISCORDCPP_SRC})

include(GoogleTest)

gtest_discover_tests(unit_test)