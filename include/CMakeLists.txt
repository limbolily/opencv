file(GLOB old_hdrs "opencv/*.h*")
#install(FILES ${old_hdrs}
#    DESTINATION ${OPENCV_INCLUDE_INSTALL_PATH}/opencv
#    COMPONENT main)
#install(FILES "opencv2/opencv.hpp"
#    DESTINATION ${OPENCV_INCLUDE_INSTALL_PATH}/opencv2
#    COMPONENT main)
yong_install_header_files(OpenCV "opencv" ${old_hdrs})
yong_install_header_files(OpenCV "opencv2" "opencv2/opencv.hpp")
