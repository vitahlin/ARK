file(GLOB AFProto_SRC *.h *.hpp *.cpp *.cc *.c cpp/*.h cpp/*.hpp cpp/*.cpp cpp/*.cc cpp/*.c)

add_library(AFProto SHARED ${AFProto_SRC})

set_target_properties(AFProto PROPERTIES PREFIX "")
set_target_properties(AFProto PROPERTIES OUTPUT_NAME_DEBUG "AFProto_d")
set_target_properties(AFProto PROPERTIES
    FOLDER "SDK"
    ARCHIVE_OUTPUT_DIRECTORY ${SDK_OUTPUT_DIR}
    RUNTIME_OUTPUT_DIRECTORY ${SDK_OUTPUT_DIR}
    LIBRARY_OUTPUT_DIRECTORY ${SDK_OUTPUT_DIR}
)

if(UNIX)
    target_link_libraries(AFProto)
    add_definitions(
        -DLIBPROTOC_EXPORTS
        -DPROTOBUF_USE_DLLS)
else()
    target_link_libraries(AFProto
        debug libprotobufd
        optimized libprotobuf
    )
    
    add_definitions(
        -D_USRDLL
        -D_LIB
        -DLIBPROTOC_EXPORTS
        -DPROTOBUF_USE_DLLS)
endif()
