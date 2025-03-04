# ======================================================================
#  larexamples main build file
#
#  cd .../path/to/build/directory
#  source .../path/to/larexamples/ups/setup_for_development <-d|-p>
#  buildtool [-I /install/path] -bt[i] -jN
# ======================================================================

cmake_minimum_required(VERSION 3.19 FATAL_ERROR)

project(larexamples VERSION 09.03.14 LANGUAGES CXX)

# cetbuildtools contains our cmake modules
find_package(cetbuildtools REQUIRED)

include(CetCMakeEnv)
cet_cmake_env()

cet_set_compiler_flags(DIAGS CAUTIOUS
  WERROR
  NO_UNDEFINED
  EXTRA_FLAGS -pedantic -Wno-unused-local-typedefs
)

cet_report_compiler_flags()

find_package(cetlib_except REQUIRED PUBLIC)
find_package(cetlib REQUIRED PUBLIC)
find_package(fhiclcpp REQUIRED PUBLIC)
find_package(messagefacility REQUIRED PUBLIC)
find_package(canvas_root_io REQUIRED)
find_package(art REQUIRED PUBLIC)
find_package(art_root_io REQUIRED PUBLIC)
find_package(nusimdata REQUIRED PUBLIC)
find_package(Boost REQUIRED)
find_package(ROOT COMPONENTS Core  RIO Tree Hist MathCore Physics REQUIRED PUBLIC)
# these are minimum required versions, not the actual product versions
find_ups_product( larcoreobj )
find_ups_product( larcorealg )
find_ups_product( larcore )
find_ups_product( lardataobj )
find_ups_product( lardataalg )
find_ups_product( lardata )
find_ups_product( larevt )
find_ups_product( larsim )
#find_ups_product( nutools )

# macros for dictionary and simple_plugin
include(ArtDictionary)
include(ArtMake)
include(BuildPlugins)

# source
add_subdirectory(larexamples)
add_subdirectory(test)

# ups - table and config files
add_subdirectory(ups)

# packaging utility
include(UseCPack)


