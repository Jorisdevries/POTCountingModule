# use cmake 2.8 or later
cmake_minimum_required (VERSION 2.8)

project(pot_counting)

# cetbuildtools contains our cmake modules
SET ( CETBUILDTOOLS_VERSION $ENV{CETBUILDTOOLS_VERSION} )
IF (NOT CETBUILDTOOLS_VERSION)
    MESSAGE (FATAL_ERROR "ERROR: setup cetbuildtools to get the cmake modules")
    ENDIF()

    set(CMAKE_MODULE_PATH $ENV{ART_DIR}/Modules
                  $ENV{CETBUILDTOOLS_DIR}/Modules
                                ${CMAKE_MODULE_PATH})

    include(CetCMakeEnv)
    cet_cmake_env()

    cet_set_compiler_flags(DIAGS CAUTIOUS
      WERROR
        NO_UNDEFINED
          ALLOW_DEPRECATIONS
            EXTRA_FLAGS -pedantic -Wno-unused-local-typedefs -std=c++1y
            )

    cet_report_compiler_flags()

# these are minimum required versions, not the actual product versions
find_ups_product( larcore v1_00_00 )
find_ups_product( lardata v1_00_00 )
find_ups_product( larevt v1_00_00 )
find_ups_product( larsim v1_00_00 )
find_ups_product( larreco v1_00_00 )
find_ups_product( nutools v0_00_00 )
find_ups_product( art v1_09_00 )
find_ups_product( pandora v02_00_00 )
find_ups_product( larpandoracontent v02_04_00 )
find_ups_product( cetbuildtools v4_09_00 )
find_ups_product( postgresql v9_1_5 )


# macros for dictionary and simple_plugin
include(ArtDictionary)
include(ArtMake)
include(BuildPlugins)

# source
add_subdirectory(pot_counting)

# ups - table and config files
add_subdirectory(ups)

# packaging utility
include(UseCPack)
