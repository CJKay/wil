
include(${CMAKE_SOURCE_DIR}/cmake/common_build_flags.cmake)

# TODO: Might be worth trying to conditionally do this on SDK version, assuming there's a semi-easy way to detect that
include_directories(BEFORE SYSTEM ./workarounds/wrl)

# The build pipelines have limitations that local development environments do not, so turn a few knobs
if (${FAST_BUILD})
    replace_cxx_flag("/GR" "/GR-") # Disables RTTI
    add_definitions(-DCATCH_CONFIG_FAST_COMPILE -DWIL_FAST_BUILD)
endif()

add_subdirectory(app)
add_subdirectory(cpplatest)
add_subdirectory(noexcept)
add_subdirectory(normal)
add_subdirectory(win7)
