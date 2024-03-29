project (TakarEngine)

# -----------------------------------------------------------------------------

find_package (OpenGL REQUIRED)
include_directories (${OPENGL_INCLUDE_DIRS})

# -----------------------------------------------------------------------------

set (HEADER_FILES 
     # geometry
     public/geometry/bounding_box.h
	 public/geometry/mesh.h
     public/geometry/rect.h
     public/geometry/quad.h
     public/geometry/sphere.h
     public/geometry/triangle.h
     public/geometry/voxel.h
     # .
     public/image.h
     # rendering
     public/rendering/camera.h
     public/rendering/color.h
	 public/rendering/node.h
     public/rendering/path_tracer.h
     public/rendering/ray.h
     public/rendering/renderable.h
     public/rendering/scene.h
     public/rendering/viewport.h
	 )

set (IMPL_FILES
    # geometry
    impl/geometry/mesh.cpp
    impl/geometry/quad.cpp
    impl/geometry/rect.cpp
    impl/geometry/sphere.cpp
    impl/geometry/triangle.cpp
    impl/geometry/voxel.cpp
    # .
    impl/image.cpp
    # rendering
    impl/rendering/camera.cpp
    impl/rendering/node.cpp
    impl/rendering/path_tracer.cpp
    impl/rendering/ray.cpp
    impl/rendering/scene.cpp
    impl/rendering/viewport.cpp
    )

source_group (TakarEngine
    FILES
    public/image.h
    impl/image.cpp
    )

source_group (geometry
    FILES
    public/geometry/bounding_box.h
    public/geometry/mesh.h
    impl/geometry/mesh.cpp
    public/geometry/quad.h
    impl/geometry/quad.cpp
    public/geometry/rect.h
    impl/geometry/rect.cpp
    public/geometry/sphere.h
    impl/geometry/sphere.cpp
    public/geometry/triangle.h
    impl/geometry/triangle.cpp
    public/geometry/voxel.h
    impl/geometry/voxel.cpp
    )

source_group (glad
    FILES
    ../third-party/glad/src/glad.c
    )

source_group (rendering
    FILES
    public/rendering/camera.h
    impl/rendering/camera.cpp
    public/rendering/node.h
    impl/rendering/node.cpp
    public/rendering/path_tracer.h
    impl/rendering/path_tracer.cpp
    public/rendering/ray.h
    impl/rendering/ray.cpp
    public/rendering/renderable.h
    public/rendering/scene.h
    impl/rendering/scene.cpp
    public/rendering/viewport.h
    impl/rendering/viewport.cpp
    )

set (THIRD_PARTY_IMPL_FILES ../third-party/glad/src/glad.c)
set (SOURCE_FILES ${HEADER_FILES} ${IMPL_FILES} ${THIRD_PARTY_IMPL_FILES})

# -----------------------------------------------------------------------------

add_library (TakarEngine STATIC ${SOURCE_FILES})

target_include_directories (
    TakarEngine 
    PUBLIC 
    ${CMAKE_CURRENT_SOURCE_DIR}/public
    # Third-party include directories
    "../third-party/glad/include"
    "../third-party/glfw/include"
    "../third-party/mq-math/public"
    "../third-party/stb_image_clone"
    )

# -----------------------------------------------------------------------------

# To treat warning as error, uncomment the following:
if (MSVC)
  target_compile_options (TakarEngine PRIVATE /W4 /WX)
else ()
  target_compile_options (TakarEngine PRIVATE -Wall -Wextra -Wpedantic -Werror)
endif ()

# -----------------------------------------------------------------------------
