add_subdirectory(CheatTrackData)

art_make(
  LIB_LIBRARIES
    ROOT::Core
    ROOT::Physics
    lardataobj_RecoBase
    nusimdata::SimulationBase
  MODULE_LIBRARIES
    messagefacility::MF_MessageLogger
    ROOT::Core
    larexamples_Algorithms_TotallyCheatTracks
    nusimdata::SimulationBase
  )

install_headers()
install_fhicl()

# install all sources, plus CMakeLists.txt and all configuration files
file(GLOB TESTFHICLFILES
     LIST_DIRECTORIES false
     *.fcl
     )
install_source(EXTRAS ${TESTFHICLFILES})
unset(TESTFHICLFILES)

install_source()
