cmake_minimum_required(VERSION 3.14)
project(DownStream)

include(FetchContent)

set(UpStream_TAG "master")


find_package(Git QUIET)
if(GIT_FOUND)
    execute_process(
        COMMAND ${GIT_EXECUTABLE} submodule status dependabot_upstream
        WORKING_DIRECTORY ${DownStream_SOURCE_DIR}
        OUTPUT_VARIABLE GIT_SUBMODULE_STRING
        OUTPUT_STRIP_TRAILING_WHITESPACE
    )
    string(SUBSTRING "${GIT_SUBMODULE_STRING}" 0 1 SUBMODULE_PREFIX)
    string(SUBSTRING "${GIT_SUBMODULE_STRING}" 1 40 SUBMODULE_HASH)
    if ("${SUBMODULE_PREFIX}" STREQUAL "-")
        set(UpStream_TAG "${SUBMODULE_HASH}")
    endif()
endif()


FetchContent_Declare(
    UpStream
    GIT_REPOSITORY https://github.com/yhmtsai/dependabot_upstream.git
    GIT_TAG        "${UpStream_TAG}"     # or specific commit/tag
)
message("${UpStream_TAG}")
FetchContent_MakeAvailable(UpStream)