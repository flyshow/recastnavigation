file(GLOB SOURCES Source/*.cpp)

include_directories(../Recast/Include)
include_directories(../Detour/Include)
include_directories(../DetourTileCache/Include)
include_directories(Include)

if (RECASTNAVIGATION_STATIC)
    add_library(DebugUtils STATIC ${SOURCES})
else()
    add_library(DebugUtils SHARED ${SOURCES})
endif()

set_target_properties(DebugUtils PROPERTIES
        SOVERSION ${SOVERSION}
        VERSION ${VERSION}
        )
target_compile_features(DebugUtils PUBLIC cxx_std_17)

add_dependencies(DebugUtils Recast Detour)
target_link_libraries(DebugUtils Recast Detour)

install(TARGETS DebugUtils
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        COMPONENT library
        )

file(GLOB INCLUDES Include/*.h)
install(FILES ${INCLUDES} DESTINATION include)
