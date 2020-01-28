# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)

# 项目信息
project (PROJ_REPO)
# 指定top路径
get_filename_component(PROJ_REPO_TOP_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../.. ABSOLUTE)

include(GNUInstallDirs)

# 设置cmake工具路径
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH}
    ${PROJ_REPO_TOP_DIR}/modules/app/cmake)

# 设置依赖
add_subdirectory(${PROJ_REPO_TOP_DIR}/modules/core proj_core)
include_directories(${PROJ_REPO_TOP_DIR}/modules/core/inc_pub)


# 指定生成目标
add_executable(PROJ_REPO main.c)
target_link_libraries(PROJ_REPO proj_core)

# 指定安装
install(
        TARGETS                 PROJ_REPO 
        DESTINATION             "${CMAKE_INSTALL_BINDIR}"
        EXPORT                  "${TARGETS_EXPORT_NAME}"
        LIBRARY     DESTINATION "${CMAKE_INSTALL_LIBDIR}"
        ARCHIVE     DESTINATION "${CMAKE_INSTALL_LIBDIR}"
        RUNTIME     DESTINATION "${CMAKE_INSTALL_BINDIR}"
        INCLUDES    DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
    )