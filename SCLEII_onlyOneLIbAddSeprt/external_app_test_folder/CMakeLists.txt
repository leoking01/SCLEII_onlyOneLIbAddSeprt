project(TestInstallation)
cmake_minimum_required(VERSION 3.5)

find_package(MyMath 1.0  PATHS  "E:\\AAAAA_cmk_lib_export\\SCLEII_onlyOneLIbAddSeprt_19.0.24215.1_install")

add_executable(mymathApp mymathApp.cc)
target_link_libraries(mymathApp MyMath::mymath)
target_include_directories(mymathApp  PRIVATE  "E:\\AAAAA_cmk_lib_export\\SCLEII_onlyOneLIbAddSeprt_19.0.24215.1_install/include")
