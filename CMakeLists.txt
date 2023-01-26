cmake_minimum_required(VERSION 3.16)

find_package(Java REQUIRED)
include(UseJava)

# enable_testing()

project(jlox)

set(CMAKE_JAVA_COMPILE_FLAGS, "-source" "1.6" "-target" "1.6")

add_jar(jlox 
	SOURCES
		${CMAKE_CURRENT_SOURCE_DIR}/lox/Lox.java
		${CMAKE_CURRENT_SOURCE_DIR}/lox/Scanner.java
		${CMAKE_CURRENT_SOURCE_DIR}/lox/Token.java
		${CMAKE_CURRENT_SOURCE_DIR}/lox/TokenType.java
		${CMAKE_CURRENT_SOURCE_DIR}/lox/Expr.java
		${CMAKE_CURRENT_SOURCE_DIR}/lox/Stmt.java
		${CMAKE_CURRENT_SOURCE_DIR}/lox/AstPrinter.java
		${CMAKE_CURRENT_SOURCE_DIR}/lox/Parser.java
		${CMAKE_CURRENT_SOURCE_DIR}/lox/RuntimeError.java
		${CMAKE_CURRENT_SOURCE_DIR}/lox/Interpreter.java
		${CMAKE_CURRENT_SOURCE_DIR}/lox/Environment.java
		${CMAKE_CURRENT_SOURCE_DIR}/lox/LoxCallable.java
		${CMAKE_CURRENT_SOURCE_DIR}/lox/LoxFunction.java
		${CMAKE_CURRENT_SOURCE_DIR}/lox/Return.java
	MANIFEST
		${CMAKE_CURRENT_SOURCE_DIR}/lox/MANIFEST.MF)

add_custom_command(
	OUTPUT
		${CMAKE_CURRENT_SOURCE_DIR}/lox/Expr.java
		${CMAKE_CURRENT_SOURCE_DIR}/lox/Stmt.java
	DEPENDS
		${CMAKE_CURRENT_SOURCE_DIR}/tool/GenerateAst.java
	COMMAND
		java -jar ${CMAKE_BINARY_DIR}/generate_ast.jar ${CMAKE_CURRENT_SOURCE_DIR}/lox)

add_jar(generate_ast
	SOURCES
		${CMAKE_CURRENT_SOURCE_DIR}/tool/GenerateAst.java
	MANIFEST
		${CMAKE_CURRENT_SOURCE_DIR}/tool/MANIFEST.MF)

get_target_property(_jarFile jlox JAR_FILE)
get_target_property(_classDir jlox CLASSDIR)

get_target_property(_jarFile generate_ast JAR_FILE)
get_target_property(_classDir generate_ast CLASSDIR)

message(STATUS "Jar file ${_jarFile}")
message(STATUS "Class compiled to ${_classDir}")

#add_test()
