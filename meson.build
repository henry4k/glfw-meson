project('glfw', 'c',
    version: '3.3.0',
    license: 'zlib')

thread_dep = dependency('threads')
#vulkan_dep = dependency('vulkan', required: false) # TODO
# # Dependencies required by the MoltenVK static library
# set(GLFW_VULKAN_DEPS
#     "-lc++"
#     "-framework Cocoa"
#     "-framework Metal"
#     "-framework QuartzCore")


#--------------------------------------------------------------------
# Set compiler specific flags
#--------------------------------------------------------------------

compiler_id = meson.get_compiler('c').get_id()

if compiler_id == 'msvc'
    if get_option('glfw_use_msvc_runtime_library_dll')
        #foreach (flag CMAKE_C_FLAGS
        #              CMAKE_C_FLAGS_DEBUG
        #              CMAKE_C_FLAGS_RELEASE
        #              CMAKE_C_FLAGS_MINSIZEREL
        #              CMAKE_C_FLAGS_RELWITHDEBINFO)
        #    if (${flag} MATCHES "/MD")
        #        string(REGEX REPLACE "/MD" "/MT" ${flag} "${${flag}}")
        #    endif()
        #    if (${flag} MATCHES "/MDd")
        #        string(REGEX REPLACE "/MDd" "/MTd" ${flag} "${${flag}}")
        #    endif()
        #endforeach()
    endif
endif


#--------------------------------------------------------------------
# Detect and select backend APIs
#--------------------------------------------------------------------

host_system = host_machine.system()

if host_system == 'windows' or host_system == 'cygwin'
    default_backend = 'win32'
elif host_system == 'darwin'
    default_backend = 'cocoa'
elif host_system == 'linux' or host_system == 'bsd'
    default_backend = 'x11'
endif
backend = get_option('glfw_backend', default_backend)


#--------------------------------------------------------------------
# Add Vulkan static library if requested
#--------------------------------------------------------------------

if get_option('glfw_vulkan_static')
    #if (VULKAN_FOUND AND VULKAN_STATIC_LIBRARY)
    #    list(APPEND glfw_LIBRARIES "${VULKAN_STATIC_LIBRARY}" ${GLFW_VULKAN_DEPS})
    #    if (BUILD_SHARED_LIBS)
    #        message(WARNING "Linking Vulkan loader static library into GLFW")
    #    endif()
    #else()
    #    if (BUILD_SHARED_LIBS OR GLFW_BUILD_EXAMPLES OR GLFW_BUILD_TESTS)
    #        message(FATAL_ERROR "Vulkan loader static library not found")
    #    else()
    #        message(WARNING "Vulkan loader static library not found")
    #    endif()
    #endif()
endif


#--------------------------------------------------------------------
# Find and add Unix math and time libraries
#--------------------------------------------------------------------

if host_system == 'linux' or host_system == 'bsd'
    rt_library = find_library('rt', required: false)
    math_library = find_library('m', required: false)
    dl_library = find_library('dl', required: false)
endif


#--------------------------------------------------------------------
# Get backend dependencies
#--------------------------------------------------------------------

if backend == 'win32'
    gdi32_library = find_library('gdi32')
elif backend == 'x11'
    x11_dependency = dependency('X11')
    # TODO: XRandR header found?
    # TODO: Xinerama header found?
    # TODO: Xkb header found?
    # TODO: Xcursor header found?
elif backend == 'wayland'
    ecm_dependency = dependency('ECM')
    wayland_dependency = dependency('Wayland')
    wayland_scanner_dependency = dependency('WaylandScanner')
    wayland_protocols_dependency = dependency('WaylandProtocols', version: '1.1')
    wayland_egl_dependency = dependency('wayland-egl')
    xkbcommon_dependency = dependency('xkbcommon')
elif backend == 'mir'
    mir_dependency = dependency('mirclient')
    xkbcommon_dependency = dependency('xkbcommon')
elif backend == 'osmesa'
    osmesa_dependency = dependency('OSMesa')
elif backend == 'cocoa'
    #list(APPEND glfw_LIBRARIES
    #    "-framework Cocoa"
    #    "-framework IOKit"
    #    "-framework CoreFoundation"
    #    "-framework CoreVideo")
endif


#--------------------------------------------------------------------
# Create generated files
#--------------------------------------------------------------------

conf_data = configuration_data()
configure_file(input:  'src/glfw_config.h.in',
               output: 'src/glfw_config.h',
               configuration: conf_data)
configure_file(input:  'src/glfw3.pc.in',
               output: 'src/glfw3.pc',
               configuration: conf_data)


#--------------------------------------------------------------------
# Add subdirectories
#--------------------------------------------------------------------

subdir('src')


#--------------------------------------------------------------------
# Install files other than the library
# The library is installed by src/CMakeLists.txt
#--------------------------------------------------------------------

#if (GLFW_INSTALL)
#    install(DIRECTORY include/GLFW DESTINATION include
#            FILES_MATCHING PATTERN glfw3.h PATTERN glfw3native.h)
#
#    install(FILES "${GLFW_BINARY_DIR}/src/glfw3Config.cmake"
#                  "${GLFW_BINARY_DIR}/src/glfw3ConfigVersion.cmake"
#            DESTINATION "${GLFW_CONFIG_PATH}")
#
#    install(EXPORT glfwTargets FILE glfw3Targets.cmake
#            EXPORT_LINK_INTERFACE_LIBRARIES
#            DESTINATION "${GLFW_CONFIG_PATH}")
#    install(FILES "${GLFW_BINARY_DIR}/src/glfw3.pc"
#            DESTINATION "lib${LIB_SUFFIX}/pkgconfig")
#
#    # Only generate this target if no higher-level project already has
#    if (NOT TARGET uninstall)
#        configure_file(cmake_uninstall.cmake.in
#                       cmake_uninstall.cmake IMMEDIATE @ONLY)
#
#        add_custom_target(uninstall
#                          "${CMAKE_COMMAND}" -P
#                          "${GLFW_BINARY_DIR}/cmake_uninstall.cmake")
#    endif()
#endif()


# vim: set softtabstop=4 shiftwidth=4:
