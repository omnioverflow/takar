project (RunTakar)

find_package (OpenGL REQUIRED)
include_directories (${OPENGL_INCLUDE_DIRS})

# -----------------------------------------------------------------------------

set (SOURCE_FILES main.cpp)
add_executable (${PROJECT_NAME} ${SOURCE_FILES})

# -----------------------------------------------------------------------------

# set VS startup project
set_property (
    DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} 
    PROPERTY VS_STARTUP_PROJECT ${PROJECT_NAME}
    )

# Get the Engine include directories
get_target_property (
    MAIN_LIBRARY_INCLUDES TakarEngine
    INCLUDE_DIRECTORIES
    )

# -----------------------------------------------------------------------------

target_include_directories (
    ${PROJECT_NAME} 
    PUBLIC ${MAIN_LIBRARY_INCLUDES}
    )

target_link_libraries (RunTakar TakarEngine)
target_link_libraries (RunTakar glfw)