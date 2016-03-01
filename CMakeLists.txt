cmake_minimum_required(VERSION 3.4)
project(oneclick)

include(cmake/detect_version.cmake)

if(CMAKE_COMPILER_IS_GNUCXX OR ${CMAKE_CXX_COMPILER_ID} STREQUAL Clang)
    add_compile_options(-std=c++11 -Wall -Wextra)

    # static build option is currently available only for linux
    option(STATIC_BUILD "Produce static buils" OFF)
endif()

 # === static build? (applicable only on linux compilers) ===
 if(STATIC_BUILD)
    SET(CMAKE_FIND_LIBRARY_SUFFIXES ".a")
    SET(BUILD_SHARED_LIBRARIES OFF)
    SET(CMAKE_EXE_LINKER_FLAGS "-static")
endif()

add_subdirectory(tinyXML)


# === source files ===
set(SOURCES
    src/ConfigParser.cpp
    src/FileGenerator.cpp
    src/main.cpp
    src/OneclickConstants.cpp
    src/ResultProcessor.cpp
    src/XMLproc.cpp
    # === project files ===
    eacirc/projects/estream/EstreamCiphers.cpp
    eacirc/projects/sha3/Sha3Functions.cpp
    eacirc/projects/caesar/CaesarCiphers.cpp
)

# === header files ===
set(HEADERS
    src/AvgValPostPr.h
    src/ConfigParser.h
    src/dirent.h
    src/FileGenerator.h
    src/FileLogger.hpp
    src/FileSystem.h
    src/OneclickConstants.h
    src/PostProcessor.h
    src/PValuePostPr.h
    src/ResultProcessor.h
    src/Utils.h
    src/XMLproc.h
    # === project files ===
    eacirc/projects/estream/EstreamCiphers.h
    eacirc/projects/sha3/Sha3Functions.h
    eacirc/projects/caesar/CaesarCiphers.h
    # === version file ===
    src/Version.h
)

set(OTHER_FILES
    run/config_samples/clean_config_sample.xml
    run/config_samples/old_settings_random_test.xml
    run/config_samples/old_settings_estream_recomp.xml
    run/config_samples/old_settings_sha3_recomp.xml
    run/script_samples/download_script_sample.pl
    run/script_samples/upload_script_sample.pl
)

# === configure files ===
detect_version(src/Version.h)

# === source groups ===
source_group(projects REGULAR_EXPRESSION "${PROJECTS_DIR}/.*")
source_group(scripts REGULAR_EXPRESSION "run/script_samples/.*")
source_group(configs REGULAR_EXPRESSION "run/config_samples/.*")

# === oneclick target ===
add_executable(oneclick ${SOURCES} ${HEADERS} ${OTHER_FILES})
target_include_directories(oneclick PRIVATE eacirc/eacirc eacirc/projects)
target_link_libraries(oneclick tinyXML)

# === build target to oneclick run directory ===
set_target_properties(oneclick PROPERTIES RUNTIME_OUTPUT_DIRECTORY run)
add_custom_command(TARGET oneclick POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_CURRENT_SOURCE_DIR}/run $<TARGET_FILE_DIR:oneclick>
)
