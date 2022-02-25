cet_make_library(LIBRARY_NAME_VAR libtarget  SOURCE MarqFitAlg.cxx )

if( ${CMAKE_HOST_SYSTEM_VERSION} MATCHES "^2.6.32.*" )
  # even if OpenMP is found on a SLF6 machine, it cannot be used.
  # see the discussion in https://cdcvs.fnal.gov/redmine/issues/23001
  message(STATUS "OpenMP is not supported on SLF6")
else()
  find_package(OpenMP EXPORT)
  if(OPENMP_FOUND)
    target_link_libraries(${libtarget} PUBLIC OpenMP::OpenMP_CXX)
  endif(OPENMP_FOUND)
endif()

install_headers()
install_fhicl()
install_source()
