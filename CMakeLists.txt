cmake_minimum_required(VERSION 3.16)

find_package(Java REQUIRED)
include(UseJava)

# enable_testing()

project(jlox)

set(CMAKE_JAVA_COMPILE_FLAGS, "-source" "1.6" "-target" "1.6")

add_jar(jlox 
	SOURCES
		${CMAKE_CURRENT_SOURCE_DIR}/Lox.java
		${CMAKE_CURRENT_SOURCE_DIR}/Scanner.java
		${CMAKE_CURRENT_SOURCE_DIR}/Token.java
		${CMAKE_CURRENT_SOURCE_DIR}/TokenType.java
	MANIFEST
		${CMAKE_CURRENT_SOURCE_DIR}/MANIFEST.MF)

get_target_property(_jarFile jlox JAR_FILE)
get_target_property(_classDir jlox CLASSDIR)

message(STATUS "Jar file ${_jarFile}")
message(STATUS "Class compiled to ${_classDir}")

#add_test()
