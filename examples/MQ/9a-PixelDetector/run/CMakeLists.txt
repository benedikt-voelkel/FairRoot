 ################################################################################
 #    Copyright (C) 2014 GSI Helmholtzzentrum fuer Schwerionenforschung GmbH    #
 #                                                                              #
 #              This software is distributed under the terms of the             # 
 #         GNU Lesser General Public Licence version 3 (LGPL) version 3,        #  
 #                  copied verbatim in the file "LICENSE"                       #
 ################################################################################

Set(MaxTestTime 30)

GENERATE_TEST_SCRIPT(${CMAKE_BINARY_DIR}/bin/examples/MQ/9a-PixelDetector/startFairMQEx9aFromBin_Static.sh ${CMAKE_CURRENT_BINARY_DIR})

Add_Test(ex9a_static
	${CMAKE_CURRENT_BINARY_DIR}/startFairMQEx9aFromBin_Static.sh --work-dir ${CMAKE_BINARY_DIR} --max-index 10000 --aggregate 100 --processors 5 --force-kill true)
Set_Tests_Properties(ex9a_static PROPERTIES DEPENDS ex9_static)
Set_Tests_Properties(ex9a_static PROPERTIES TIMEOUT ${MaxTestTime})
Set_Tests_Properties(ex9a_static PROPERTIES PASS_REGULAR_EXPRESSION "Shell script finished successfully")

set(INCLUDE_DIRECTORIES
    ${BASE_INCLUDE_DIRECTORIES}
    ${CMAKE_SOURCE_DIR}/fairmq
    ${CMAKE_SOURCE_DIR}/fairmq/devices
    ${CMAKE_SOURCE_DIR}/fairmq/options
    ${CMAKE_SOURCE_DIR}/fairmq/tools
    ${CMAKE_SOURCE_DIR}/base/MQ/policies/Sampler
    ${CMAKE_SOURCE_DIR}/base/MQ/policies/Serialization
    ${CMAKE_SOURCE_DIR}/base/MQ/policies/Storage
    ${CMAKE_SOURCE_DIR}/base/MQ/baseMQtools
    ${CMAKE_SOURCE_DIR}/examples/MQ/9-PixelDetector
    ${CMAKE_SOURCE_DIR}/examples/MQ/9-PixelDetector/src
    ${CMAKE_SOURCE_DIR}/examples/MQ/9a-PixelDetector/src
    ${CMAKE_SOURCE_DIR}/examples/MQ/9a-PixelDetector/src/devices
)

Set(SYSTEM_INCLUDE_DIRECTORIES
    ${SYSTEM_INCLUDE_DIRECTORIES}
    ${ZeroMQ_INCLUDE_DIR}
)

include_directories(${INCLUDE_DIRECTORIES})
include_directories(SYSTEM ${SYSTEM_INCLUDE_DIRECTORIES})

set(NETWORK_INTERFACE eth0)
If(APPLE)
  set(NETWORK_INTERFACE lo0)
EndIf(APPLE)

set(EXAMPLE9_FILE_LOCATION ${CMAKE_SOURCE_DIR})
set(EXAMPLE9_BIN_LOCATION  ${CMAKE_BINARY_DIR}/bin/examples/MQ/9-PixelDetector)
set(EXAMPLE9a_FILE_LOCATION ${CMAKE_SOURCE_DIR})
set(EXAMPLE9a_BIN_LOCATION  ${CMAKE_BINARY_DIR}/bin/examples/MQ/9a-PixelDetector)
set(FAIRROOT_BIN_LOCATION  ${CMAKE_BINARY_DIR}/bin)

configure_file( ${CMAKE_SOURCE_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromRoot.sh.in                
		${CMAKE_BINARY_DIR}/bin/examples/MQ/9a-PixelDetector/startFairMQEx9aFromRoot.sh )
configure_file( ${CMAKE_SOURCE_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromRoot_Static.sh.in                
		${CMAKE_BINARY_DIR}/bin/examples/MQ/9a-PixelDetector/startFairMQEx9aFromRoot_Static.sh )
configure_file( ${CMAKE_SOURCE_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromBin.sh.in                
		${CMAKE_BINARY_DIR}/bin/examples/MQ/9a-PixelDetector/startFairMQEx9aFromBin.sh )
configure_file( ${CMAKE_SOURCE_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromBin_Static.sh.in                
		${CMAKE_BINARY_DIR}/bin/examples/MQ/9a-PixelDetector/startFairMQEx9aFromBin_Static.sh )
configure_file( ${CMAKE_SOURCE_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aToBin.sh.in                
		${CMAKE_BINARY_DIR}/bin/examples/MQ/9a-PixelDetector/startFairMQEx9aToBin.sh )

set(EXAMPLE9_FILE_LOCATION ${CMAKE_INSTALL_PREFIX}/share/fairbase)
set(EXAMPLE9_BIN_LOCATION  ${CMAKE_INSTALL_PREFIX}/share/fairbase/examples/MQ/9-PixelDetector/bin)
set(EXAMPLE9a_FILE_LOCATION ${CMAKE_INSTALL_PREFIX}/share/fairbase)
set(EXAMPLE9a_BIN_LOCATION  ${CMAKE_INSTALL_PREFIX}/share/fairbase/examples/MQ/9a-PixelDetector/bin)
set(FAIRROOT_BIN_LOCATION  ${CMAKE_INSTALL_PREFIX}/bin)

configure_file( ${CMAKE_SOURCE_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromRoot.sh.in      
		${CMAKE_BINARY_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromRoot.sh_install )
configure_file( ${CMAKE_SOURCE_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromRoot_Static.sh.in      
		${CMAKE_BINARY_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromRoot_Static.sh_install )
configure_file( ${CMAKE_SOURCE_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromBin.sh.in      
		${CMAKE_BINARY_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromBin.sh_install )
configure_file( ${CMAKE_SOURCE_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromBin_Static.sh.in      
		${CMAKE_BINARY_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromBin_Static.sh_install )
configure_file( ${CMAKE_SOURCE_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aToBin.sh.in      
		${CMAKE_BINARY_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aToBin.sh_install )

set(EXAMPLE9_INSTALL_BIN share/fairbase/examples/MQ/9a-PixelDetector/bin)
set(EXAMPLE9a_INSTALL_BIN share/fairbase/examples/MQ/9a-PixelDetector/bin)

Install(FILES ${CMAKE_BINARY_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromRoot.sh_install
        DESTINATION ${EXAMPLE9a_INSTALL_BIN}
        RENAME startFairMQEx9aFromRoot.sh PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ WORLD_READ)
Install(FILES ${CMAKE_BINARY_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromRoot_Static.sh_install
        DESTINATION ${EXAMPLE9a_INSTALL_BIN}
        RENAME startFairMQEx9aFromRoot_Static.sh PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ WORLD_READ)
Install(FILES ${CMAKE_BINARY_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromBin.sh_install
        DESTINATION ${EXAMPLE9a_INSTALL_BIN}
        RENAME startFairMQEx9aFromBin.sh PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ WORLD_READ)
Install(FILES ${CMAKE_BINARY_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aFromBin_Static.sh_install
        DESTINATION ${EXAMPLE9a_INSTALL_BIN}
        RENAME startFairMQEx9aFromBin_Static.sh PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ WORLD_READ)
Install(FILES ${CMAKE_BINARY_DIR}/examples/MQ/9a-PixelDetector/run/scripts/startFairMQEx9aToBin.sh_install
        DESTINATION ${EXAMPLE9a_INSTALL_BIN}
        RENAME startFairMQEx9aToBin.sh PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ WORLD_READ)


set(LINK_DIRECTORIES
    ${ROOT_LIBRARY_DIR}
    ${Boost_LIBRARY_DIRS}
)

link_directories(${LINK_DIRECTORIES})


Set(Exe_Names
    ex9a-samplerBin
    ex9a-sinkBin
    ex9a-processorBin
)

set(Exe_Source
    runEx9aSamplerBin.cxx
    runEx9aFileSinkBin.cxx
    runEx9aTaskProcessorBin.cxx
)


List(LENGTH Exe_Names _length)
Math(EXPR _length ${_length}-1)


set(BIN_DESTINATION share/fairbase/examples/MQ/9a-PixelDetector/bin)
set(EXECUTABLE_OUTPUT_PATH "${EXECUTABLE_OUTPUT_PATH}/examples/MQ/9a-PixelDetector")

ForEach(_file RANGE 0 ${_length})
    List(GET Exe_Names ${_file} _name)
    List(GET Exe_Source ${_file} _src)
    Set(EXE_NAME ${_name})
    Set(SRCS ${_src})
    Set(DEPENDENCIES Pixel PixelAlt)
    GENERATE_EXECUTABLE()
EndForEach(_file RANGE 0 ${_length})
