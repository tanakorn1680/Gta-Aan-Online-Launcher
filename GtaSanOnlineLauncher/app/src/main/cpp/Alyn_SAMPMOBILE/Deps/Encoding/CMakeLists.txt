cmake_minimum_required(VERSION 3.22.1)
project(Encoding)

file(GLOB INCLUDE_FILES
        include/*.h
)

file(GLOB SOURCE_FILES
        encoding.cpp
)

add_library(${PROJECT_NAME} INTERFACE)

target_sources(${PROJECT_NAME} INTERFACE
        ${INCLUDE_FILES}
        ${SOURCE_FILES})


set(iconv_path "${CMAKE_CURRENT_SOURCE_DIR}/lib/${ANDROID_ABI}/libiconv.a")
add_library(iconv STATIC IMPORTED)
set_target_properties(iconv PROPERTIES
    IMPORTED_LOCATION ${iconv_path}
    MAP_IMPORTED_CONFIG_RELWITHDEBINFO Release
    MAP_IMPORTED_CONFIG_MINSIZEREL Release)

set(charset_path "${CMAKE_CURRENT_SOURCE_DIR}/lib/${ANDROID_ABI}/libcharset.a")
add_library(charset STATIC IMPORTED)
set_target_properties(charset PROPERTIES
    IMPORTED_LOCATION ${charset_path}
    MAP_IMPORTED_CONFIG_RELWITHDEBINFO Release
    MAP_IMPORTED_CONFIG_MINSIZEREL Release)

target_link_libraries(${PROJECT_NAME} INTERFACE
        iconv
        charset
)

target_include_directories(${PROJECT_NAME} INTERFACE
        "${CMAKE_CURRENT_SOURCE_DIR}/include"
)
