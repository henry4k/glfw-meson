test_link_args = []
if cc.get_id() == 'msvc'
    test_link_args += '/ENTRY:mainCRTStartup' # use main() instead of WinMain()
endif

test_deps = [glfw_dep, glad_dep, math_dep]


foreach t : [['clipboard', [getopt_dep]],
             ['events',    [getopt_dep]],
             ['msaa',      [getopt_dep]],
             ['glfwinfo',  [getopt_dep]],
             ['iconify',   [getopt_dep]],
             ['monitors',  [getopt_dep]],
             ['reopen',    []],
             ['cursor',    []],
             ['empty',     [tinycthread_dep, rt_dep]],
             ['gamma',     []],
             ['icon',      []],
             ['inputlag',  [getopt_dep]],
             ['joysticks', []],
             ['sharing',   [getopt_dep]],
             ['tearing',   [getopt_dep]],
             ['threads',   [tinycthread_dep, rt_dep]],
             ['timeout',   []],
             ['title',     []],
             ['windows',   [getopt_dep]]]
    executable(t[0],
               t[0]+'.c',
               link_args: test_link_args,
               dependencies: test_deps + t[1])
endforeach

#if (VULKAN_FOUND)
#    add_executable(vulkan WIN32 vulkan.c ${ICON})
#    target_include_directories(vulkan PRIVATE "${VULKAN_INCLUDE_DIR}")
#    if (GLFW_VULKAN_STATIC)
#        target_link_libraries(vulkan "${VULKAN_STATIC_LIBRARY}" ${GLFW_VULKAN_DEPS})
#    else()
#        target_link_libraries(vulkan "${VULKAN_LIBRARY}")
#    endif()
#    list(APPEND WINDOWS_BINARIES vulkan)
#endif()
