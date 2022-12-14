# 如果想生成静态库，使用下面的语句
# add_library(mymath mymath.cc)
# target_include_directories(mymath PUBLIC ${CMAKE_SOURCE_DIR}/include)

# 如果想生成动态库，使用下面的语句
add_library(mymath SHARED mymath.cc)
target_include_directories(mymath PRIVATE  ${CMAKE_SOURCE_DIR}/mymath/include)
set_target_properties(mymath PROPERTIES PUBLIC_HEADER ${CMAKE_SOURCE_DIR}/mymath/include/mymath.h)

# 写入库的版本信息
include(CMakePackageConfigHelpers)
write_basic_package_version_file(
        MyMathConfigVersion.cmake
        VERSION ${PACKAGE_VERSION}
        COMPATIBILITY AnyNewerVersion
        )

# 将库文件，可执行文件，头文件安装到指定目录
install(TARGETS mymath
        EXPORT MyMathTargets
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin
        PUBLIC_HEADER DESTINATION include
        )

# 将库的相关信息输出为MyMathConfig.cmake，供find_package查找
install(EXPORT MyMathTargets
        FILE MyMathTargets.cmake
        NAMESPACE MyMath::
        DESTINATION lib/cmake/mymath
        )

configure_file(MyMathConfig.cmake.in mymath/MyMathConfig.cmake @ONLY)
install(FILES "${CMAKE_CURRENT_BINARY_DIR}/MyMathConfig.cmake"
                "${CMAKE_CURRENT_BINARY_DIR}/MyMathConfigVersion.cmake"
        DESTINATION lib/cmake/MyMath
        )


