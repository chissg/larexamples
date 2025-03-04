art_make(
  EXCLUDE
    PointIsolationAlg_test.cc
    PointIsolationAlgRandom_test.cc
    PointIsolationAlgStress_test.cc
  LIB_LIBRARIES
    lardataobj_RecoBase
    ROOT::Core
  MODULE_LIBRARIES
    lardataobj_RecoBase
    larcorealg_Geometry
    larcore_Geometry_Geometry_service
    larexamples_Algorithms_RemoveIsolatedSpacePoints
    test_Algorithms_RemoveIsolatedSpacePoints
    art_Framework_Core
    art::Framework_Services_Registry
    art::Framework_Principal
    art::Persistency_Provenance
    art::Utilities canvas::canvas
    messagefacility::MF_MessageLogger
    
    fhiclcpp::fhiclcpp
  )

cet_test(PointIsolationAlg_test
         LIBRARIES cetlib::cetlib
         USE_BOOST_UNIT)
cet_test(PointIsolationAlgRandom_test
         LIBRARIES cetlib::cetlib
         USE_BOOST_UNIT)

cet_test(
  PointIsolation_test
  HANDBUILT
  TEST_EXEC lar
  TEST_ARGS --rethrow-all -c point_isolation_test.fcl
  DATAFILES point_isolation_test.fcl
  )


# the following is not a real test in that it can't detect any error;
# the time taken by the stress test should be short even with debug qualifier!
cet_test(
  PointIsolationAlgStress_test
  LIBRARIES
    cetlib::cetlib
  TEST_ARGS 10000 0.05
  )

# install all sources, plus CMakeLists.txt and all configuration files
file(GLOB TESTFHICLFILES
     LIST_DIRECTORIES false
     *.fcl
     )
install_source(EXTRAS CMakeLists.txt ${TESTFHICLFILES})
unset(TESTFHICLFILES)
