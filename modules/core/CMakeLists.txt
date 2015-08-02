set(the_description "The Core Functionality")
ocv_add_module(core PRIVATE_REQUIRED "${OPENCL_LIBRARIES}" OPTIONAL opencv_cudev)
ocv_module_include_directories()

if(HAVE_WINRT)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /ZW /GS /Gm- /AI\"${WINDOWS_SDK_PATH}/References/CommonConfiguration/Neutral\" /AI\"${VISUAL_STUDIO_PATH}/vcpackages\"")
endif()

if(HAVE_CUDA)
  ocv_warnings_disable(CMAKE_CXX_FLAGS -Wundef -Wenum-compare -Wunused-function)
endif()

file(GLOB lib_cuda_hdrs        "include/opencv2/${name}/cuda/*.hpp"        "include/opencv2/${name}/cuda/*.h")
file(GLOB lib_cuda_hdrs_detail "include/opencv2/${name}/cuda/detail/*.hpp" "include/opencv2/${name}/cuda/detail/*.h")

source_group("Cuda Headers"         FILES ${lib_cuda_hdrs})
source_group("Cuda Headers\\Detail" FILES ${lib_cuda_hdrs_detail})

ocv_glob_module_sources(SOURCES "${OpenCV_BINARY_DIR}/modules/core/version_string.inc"
                        HEADERS ${lib_cuda_hdrs} ${lib_cuda_hdrs_detail})

ocv_create_module()
yong_add_dependence(OpenCV opencv_core
  DEPENDENT_PROJECT zlib
    COMMIT_HASH ${ZLIB_HASH}
    DEPENDENT_LIBS zlib)
yong_add_library_end(opencv_core)
ocv_add_precompiled_headers(${the_module})

ocv_add_accuracy_tests()
ocv_add_perf_tests()
