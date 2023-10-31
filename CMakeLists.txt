cmake_minimum_required(VERSION 3.13.0)
project(lua LANGUAGES C VERSION 5.4.6)


set(lua_compile_definition -DLUA_USE_MACOSX -DLUA_USE_READLINE)
set(lua_link_library m readline)

message(STATUS ${compile_definition})
set(lua_comiple_option -std=gnu99 -O2 -Wall -Wextra)
aux_source_directory(src liblua_src)
list(REMOVE_ITEM liblua_src "src/lua.c" "src/luac.c")

add_library(liblua ${liblua_src})
target_compile_options(liblua PRIVATE ${lua_comiple_option})
target_compile_definitions(liblua PRIVATE ${lua_compile_definition})
target_include_directories(liblua PRIVATE src include)

add_executable(luac "src/luac.c")
target_link_libraries(luac liblua)
target_compile_options(luac PRIVATE ${lua_comiple_option})
target_compile_definitions(luac PRIVATE ${lua_compile_definition})
target_include_directories(luac PRIVATE src include)

add_executable(lua "src/lua.c")
target_link_libraries(lua liblua ${lua_link_library})
target_compile_options(lua PRIVATE ${lua_comiple_option})
target_compile_definitions(lua PRIVATE ${lua_compile_definition})
target_include_directories(lua PRIVATE src include)