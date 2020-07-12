file(GLOB SOURCES Source/*.cpp)

include_directories(../Detour/Include)
include_directories(Include)

if (RECASTNAVIGATION_STATIC)
    add_library(DetourTileCache STATIC ${SOURCES})
else ()
    add_library(DetourTileCache SHARED ${SOURCES})
endif ()

set_target_properties(DetourTileCache PROPERTIES
        SOVERSION ${SOVERSION}
        VERSION ${VERSION}
        )
target_compile_features(DetourTileCache PUBLIC cxx_std_17)

add_dependencies(DetourTileCache Detour)
target_link_libraries(DetourTileCache Detour)

install(TARGETS DetourTileCache
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        COMPONENT library
        )

file(GLOB INCLUDES Include/*.h)
install(FILES ${INCLUDES} DESTINATION include)
