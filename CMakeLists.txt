# ======================================================================
#  larvecutils main build file
#
#  cd .../path/to/build/directory
#  source .../path/to/larvecutils/ups/setup_for_development <-d|-p>
#  buildtool [-I /install/path] -bt[i] -jN
# ======================================================================

cmake_minimum_required(VERSION 3.20 FATAL_ERROR)

find_package(cetmodules REQUIRED)
project(larvecutils VERSION 09.01.01 LANGUAGES CXX)

include(CetCMakeEnv)
cet_cmake_env()

cet_set_compiler_flags(DIAGS CAUTIOUS
  WERROR
  NO_UNDEFINED
  EXTRA_FLAGS -pedantic
  $<$<COMPILE_LANGUAGE:CXX>:-Wno-unused-local-typedefs>
)

cet_report_compiler_flags(REPORT_THRESHOLD VERBOSE)

# ADD SOURCE CODE SUBDIRECTORIES HERE
add_subdirectory(larvecutils)

# tests
add_subdirectory(test)

# packaging utility - must be last
cet_cmake_config()
