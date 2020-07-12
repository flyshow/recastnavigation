file(GLOB SOURCES Source/*.cpp)

include_directories(../Detour/Include)
include_directories(Include)

if (RECASTNAVIGATION_STATIC)
    add_library(DetourCrowd STATIC ${SOURCES})
else ()
    add_library(DetourCrowd SHARED ${SOURCES})
endif ()

set_target_properties(DetourCrowd PROPERTIES
        SOVERSION ${SOVERSION}
        VERSION ${VERSION}
        )
target_compile_features(DetourCrowd PUBLIC cxx_std_17)

add_dependencies(DetourCrowd Detour)
target_link_libraries(DetourCrowd Detour)

install(TARGETS DetourCrowd
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        COMPONENT library
        )

file(GLOB INCLUDES Include/*.h)
install(FILES ${INCLUDES} DESTINATION include)
