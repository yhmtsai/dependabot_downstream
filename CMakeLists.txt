cmake_minimum_required(VERSION 3.14)
project(DownStream)

include(FetchContent)

# Fetch another repository
FetchContent_Declare(
    UpStream
    GIT_REPOSITORY https://github.com/yhmtsai/dependabot_upstream.git
    GIT_TAG        master     # or specific commit/tag
)

FetchContent_MakeAvailable(UpStream)