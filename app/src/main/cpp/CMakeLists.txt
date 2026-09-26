cmake_minimum_required(VERSION 3.22.1)
project("Alyn_SAMPMOBILE")

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_C_STANDARD 11)

set(SRC_ROOT ${CMAKE_SOURCE_DIR}/Alyn_SAMPMOBILE)

file(GLOB_RECURSE ALYN_SOURCES
    "${SRC_ROOT}/*.cpp"
    "${SRC_ROOT}/*.c"
)

# ยกเว้นไฟล์ใน Deps ที่ไม่ต้อง compile ตรงๆ
list(FILTER ALYN_SOURCES EXCLUDE REGEX ".*/Deps/Opus/.*")
list(FILTER ALYN_SOURCES EXCLUDE REGEX ".*/Deps/spdlog/.*")
list(FILTER ALYN_SOURCES EXCLUDE REGEX ".*/Deps/Imgui/imgui_demo\\.cpp")

add_library(Alyn_SAMPMOBILE SHARED ${ALYN_SOURCES})

target_include_directories(Alyn_SAMPMOBILE PRIVATE
    ${SRC_ROOT}
    ${SRC_ROOT}/Deps/Bass
    ${SRC_ROOT}/Deps/Encoding/include
    ${SRC_ROOT}/Deps/Imgui
    ${SRC_ROOT}/Deps/Obfuscator
    ${SRC_ROOT}/Deps/Opus/include
    ${SRC_ROOT}/Deps/RakNet/RakNet
    ${SRC_ROOT}/Deps/Rapidjson/rapidjson
    ${SRC_ROOT}/Deps/opencv/include
    ${SRC_ROOT}/Deps/spdlog/include
    ${SRC_ROOT}/GameSA/include
    ${SRC_ROOT}/Memory/include
)

# Prebuilt libraries
add_library(memory-lib STATIC IMPORTED)
set_target_properties(memory-lib PROPERTIES
    IMPORTED_LOCATION_ARMEABI-V7A ${SRC_ROOT}/Memory/lib/armeabi-v7a/libMemory.a
    IMPORTED_LOCATION_ARM64-V8A   ${SRC_ROOT}/Memory/lib/arm64-v8a/libMemory.a
)

add_library(encoding-lib STATIC IMPORTED)
set_target_properties(encoding-lib PROPERTIES
    IMPORTED_LOCATION_ARMEABI-V7A ${SRC_ROOT}/Deps/Encoding/lib/armeabi-v7a/libiconv.a
    IMPORTED_LOCATION_ARM64-V8A   ${SRC_ROOT}/Deps/Encoding/lib/arm64-v8a/libiconv.a
)

find_library(log-lib log)
find_library(android-lib android)
find_library(gles-lib GLESv2)
find_library(egl-lib EGL)
find_library(z-lib z)

target_link_libraries(Alyn_SAMPMOBILE
    memory-lib
    encoding-lib
    ${log-lib}
    ${android-lib}
    ${gles-lib}
    ${egl-lib}
    ${z-lib}
)

# SocialClub
add_library(SocialClub SHARED
    ${CMAKE_SOURCE_DIR}/SocialClub/Main.cpp
)
target_include_directories(SocialClub PRIVATE
    ${CMAKE_SOURCE_DIR}/SocialClub
)
target_link_libraries(SocialClub ${log-lib})
