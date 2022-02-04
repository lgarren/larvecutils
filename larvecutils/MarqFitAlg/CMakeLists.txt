#include(FindOpenMP)
cet_make_library(LIBRARY_NAME_VAR libtarget  SOURCE MarqFitAlg.cxx )

if( ${CMAKE_HOST_SYSTEM_VERSION} MATCHES "^2.6.32.*" )
  message(STATUS "OpenMP is not supported on SLF6")
else()
  find_package(OpenMP)
  if(OPENMP_FOUND)
  # even if OpenMP is found on a SLF6 machine, it cannot be used.
  # see the discussion in https://cdcvs.fnal.gov/redmine/issues/23001
#    add_definitions(-DWITH_OPENMP)
#    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
#    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
#    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
    target_link_libraries(${libtarget} PUBLIC OpenMP::OpenMP_CXX)
  endif(OPENMP_FOUND)
endif()


install_headers()
install_fhicl()
install_source()
