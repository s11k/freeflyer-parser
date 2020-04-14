cmake_minimum_required(VERSION 3.2 FATAL_ERROR)

project(freeflyer-parser VERSION 0.1 LANGUAGES C)

include(GNUInstallDirs)

add_library(freeflyer-parser src/parser.c)

target_include_directories(freeflyer-parser PRIVATE src)

target_link_libraries(freeflyer-parser TreeSitter)

# 'make install' to the correct locations (provided by GNUInstallDirs).
install(TARGETS freeflyer-parser EXPORT FreeFlyerParser
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})  # This is for Windows

# This makes the project importable from the install directory
# Put config file in per-project dir (name MUST match), can also
# just go into 'cmake'.
install(EXPORT FreeFlyerParser DESTINATION share/FreeFlyerParser/cmake)

# This makes the project importable from the build directory
export(TARGETS freeflyer-parser FILE FreeFlyerParserConfig.cmake)