project(projection)

include(CMake.vars OPTIONAL)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${TESTS_INCLUDE_DIRS})
include_directories(${hermes3d_SOURCE_DIR})

add_executable(${PROJECT_NAME}
	main.cc
	${HERMES_COMMON_DIR}/trace.cc
	${HERMES_COMMON_DIR}/error.cc
)

target_link_libraries(${PROJECT_NAME} ${TESTS_LIBRARIES}) 
target_link_libraries(${PROJECT_NAME} ${HERMES_REAL_BIN})

configure_file(
	${CMAKE_CURRENT_SOURCE_DIR}/config.h.cmake
	${CMAKE_CURRENT_SOURCE_DIR}/config.h
)

#
# Tests
#

enable_testing()

set(BIN ${PROJECT_BINARY_DIR}/${PROJECT_NAME})
add_test(projection-h1-1 ${BIN} h1 ${MESHES_DIR}/mesh3d/hex1.mesh3d)
add_test(projection-h1-2 ${BIN} h1 ${MESHES_DIR}/mesh3d/hex2.mesh3d)
add_test(projection-h1-3 ${BIN} h1 ${MESHES_DIR}/mesh3d/hex4.mesh3d)
add_test(projection-h1-4 ${BIN} h1 ${MESHES_DIR}/mesh3d/hex8.mesh3d)
add_test(projection-h1-5 ${BIN} h1 ${MESHES_DIR}/mesh3d/hex27.mesh3d)
