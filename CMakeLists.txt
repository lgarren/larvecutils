# ======================================================================
#  larvecutils main build file
#
#  cd .../path/to/build/directory
#  source .../path/to/larvecutils/ups/setup_for_development <-d|-p>
#  buildtool [-I /install/path] -bt[i] -jN
# ======================================================================

cmake_minimum_required(VERSION 3.20 FATAL_ERROR) ### MIGRATE-CHANGED (migrate-3.02.01) - VERSION 3.19 -> 3.20
cmake_policy(VERSION 3.19) ### MIGRATE-ADDED (migrate-3.02.01) - CMake compatibility

find_package(cetmodules REQUIRED) ### MIGRATE-ADDED (migrate-3.02.01) - find_package(cetmodules) must precede project()
project(larvecutils VERSION 09.00.01 LANGUAGES CXX)

# cetbuildtools contains our cmake modules

include(CetCMakeEnv)
cet_cmake_env()

cet_set_compiler_flags(DIAGS CAUTIOUS
  WERROR
  NO_UNDEFINED
  EXTRA_FLAGS -pedantic
  EXTRA_CXX_FLAGS -Wno-unused-local-typedefs
)

cet_report_compiler_flags() ### MIGRATE-ACTION-RECOMMENDED (migrate-3.02.01) - add args: REPORT_THRESHOLD VERBOSE

# macros for dictionary and simple_plugin
#include(ArtDictionary)
#include(ArtMake)
#include(BuildPlugins)

# add cet_find_library commands here when needed

# ADD SOURCE CODE SUBDIRECTORIES HERE
add_subdirectory(larvecutils)

# tests
add_subdirectory(test)

# ups - table and config files
# must be AFTER all other subdirectories

# packaging utility - must be last
cet_cmake_config() ### MIGRATE-ADDED (migrate-3.02.01) - required cmd
