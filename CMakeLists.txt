# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)

# 项目信息
project (PROJ_REPO)
# 指定top路径
get_filename_component(PROJ_REPO_TOP_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../.. ABSOLUTE)

include(GNUInstallDirs)

# 设置cmake工具路径
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH}
    ${PROJ_REPO_TOP_DIR}/modules/app/cmake
    ${PROJ_REPO_TOP_DIR}/modules/core/cmake
    ${PROJ_REPO_TOP_DIR}/modules/osal/cmake
    ${PROJ_REPO_TOP_DIR}/modules/public/cmake)

# 设置依赖
find_package(Core REQUIRED)
if(NOT Core_FOUND)
    message("not found core")
endif()
include_directories(${Core_INCLUDE_DIRS})

find_package(App REQUIRED)
if(NOT App_FOUND)
    message("not found app")
endif()
include_directories(${App_INCLUDE_DIRS})

find_package(Osal REQUIRED)
if(NOT Osal_FOUND)
    message("not found osal")
endif()
include_directories(${Osal_INCLUDE_DIRS})

# 指定生成目标
add_executable(PROJ_REPO main.c)
target_link_libraries(PROJ_REPO  
    ${App_LIBRARIES} 
    ${Core_LIBRARIES}
    ${Osal_LIBRARIES})

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