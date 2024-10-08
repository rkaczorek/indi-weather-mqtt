cmake_minimum_required(VERSION 2.4.7)

if(COMMAND cmake_policy)
    cmake_policy(SET CMP0003 NEW)
endif(COMMAND cmake_policy)

PROJECT(indi-weather-mqtt CXX C)

LIST(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake_modules/")

include(GNUInstallDirs)

set (VERSION_MAJOR 1)
set (VERSION_MINOR 1)

find_package(INDI REQUIRED)
find_package(Mosquitto REQUIRED)
find_package(Threads REQUIRED)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/config.h.cmake ${CMAKE_CURRENT_BINARY_DIR}/config.h)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/indi_weather_mqtt.xml.cmake ${CMAKE_CURRENT_BINARY_DIR}/indi_weather_mqtt.xml)

include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${INDI_INCLUDE_DIR})
include(CMakeCommon)

set(indi_weather_mqtt_SRC ${CMAKE_CURRENT_SOURCE_DIR}/indi-weather-mqtt.cpp)

add_executable(indi_weather_mqtt ${indi_weather_mqtt_SRC})

target_link_libraries(indi_weather_mqtt ${INDI_LIBRARIES} ${MOSQUITTO_LIBRARIES})

IF (UNIX AND NOT APPLE)
    target_link_libraries(indi_weather_mqtt ${INDI_LIBRARIES} ${MOSQUITTO_LIBRARIES} -lpthread)
ENDIF ()

install(TARGETS indi_weather_mqtt RUNTIME DESTINATION bin )
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/indi_weather_mqtt.xml DESTINATION ${INDI_DATA_DIR})
