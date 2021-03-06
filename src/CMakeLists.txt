cmake_minimum_required(VERSION 2.8)
project(CodeRelease)

add_definitions( " -DVERSION_MAJOR=1 ")
add_definitions( " -DVERSION_MINOR=0 ")

add_definitions(-Wall -fpermissive)

find_package(qibuild)

#find_package(OpenCV REQUIRED)
#find_package(OPENCV2_CORE)
#find_package(OPENCV2_IMGPROC)
#find_package(OPENCV2_OBJDETECT)


#set(OpenCV_INCLUDES_DIRS 
#    ${OpenCV_INCLUDES}  
#    ${OPENCV2_CORE_INCLUDE_DIRS}
#    ${OPENCV2_IMGPROC_INCLUDE_DIRS}
#    ${OPENCV2_OBJDETECT_INCLUDE_DIRS})

#set(OpenCV_LIBS_DIRS 
#    ${OpenCV_LIBS}
#    ${OPENCV2_CORE_LIBRARIES}
#    ${OPENCV2_IMGPROC_LIBRARIES}
#    ${OPENCV2_OBJDETECT_LIBRARIES})

#include_directories(${OpenCV_INCLUDES_DIRS})

include_directories("Core/External/unsw")
include_directories("Core/External/unsw/unsw")

include_directories(".")
include_directories("Modules")
set(src
    main.cpp
)

set(CORE_SRC
    "Core/InitManager.cpp"
    "Core/Module.cpp"
    "Core/ModulesManager.cpp"
    "Core/SpellBook.cpp")

file(GLOB_RECURSE CORE_DRIVERS_SRC
	"Core/Drivers/*.cpp"
    "Core/Drivers/*.c"
	"Core/Drivers/*.h"
    "Core/Drivers/*.hpp")

file(GLOB_RECURSE CORE_UTILS_SRC
	"Core/Utils/*.cpp"
    "Core/Utils/*.c"
	"Core/Utils/*.h"
    "Core/Utils/*.hpp")

file(GLOB_RECURSE MODULES_SRC
	"Modules/*.cpp"
    "Modules/*.c"
	"Modules/*.h"
    "Modules/*.hpp")

add_subdirectory("Core/External")

qi_create_bin(rinobot ${src} ${CORE_SRC} ${CORE_DRIVERS_SRC} ${CORE_UTILS_SRC} ${MODULES_SRC})
qi_use_lib(rinobot unsw     
        OPENCV2_CORE 
        OPENCV2_HIGHGUI 
        OPENCV2_IMGPROC 
        OPENCV2_VIDEO 
        OPENCV2_OBJDETECT )
target_link_libraries(rinobot pthread ${OpenCV_LIBS_DIRS} TcpUdpSocket)
