set(project_name googletest)

if(DSN_GIT_SOURCE STREQUAL "xiaomi")
    set(target_url "http://git.n.xiaomi.com/pegasus/googletest.git")
else()
    set(target_url "https://github.com/imzhenyu/googletest.git")
endif()

set(my_cmake_args "-Dgtest_force_shared_crt=OFF;-DBUILD_SHARED_LIBS=ON;")

if(WIN32)
    set(target_binaries gtest.lib gtest_main.lib gtest.dll gtest_main.dll)
elseif(APPLE)
    set(target_binaries libgtest.dylib libgtest_main.dylib)
else()
    set(target_binaries libgtest.so libgtest_main.so)
endif()

include(${PROJECT_SOURCE_DIR}/bin/dsn.ext.cmake)

install(DIRECTORY ${my_source_dir}/include/gtest
    DESTINATION include/ext
    FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp" PATTERN "*.tcc" PATTERN "*.cpp"
)

set(GTEST_INCLUDE_DIR ${my_source_dir}/include PARENT_SCOPE)
set(GTEST_LIB_DIR ${my_binary_dir} PARENT_SCOPE)
