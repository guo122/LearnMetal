
if (${SLN_NAME} STREQUAL "")
	message(FATAL_ERROR "undefined project name.")
endif()

set(PROJECTNAME ${SLN_NAME})

set(IOS_TEAM "")
set(BUNDLE_IDENT "com.gzy.learnMetal")

set(SRCROOT ${CMAKE_CURRENT_LIST_DIR})
set(RESROOT ${CMAKE_CURRENT_LIST_DIR}/../res)
set(COMMON_RESROOT ${CMAKE_CURRENT_LIST_DIR}/../../CommonResources)
set(BIN_DIR ${CMAKE_ROOT_DIR}/bin)

set(DIR_SRCS 
	${SRCROOT}/AppDelegate.h
	${SRCROOT}/AppDelegate.m
	${SRCROOT}/ViewController.h
	${SRCROOT}/ViewController.m
	${SRCROOT}/LYShaderTypes.h
	${SRCROOT}/shaders.metal
	${SRCROOT}/main.m
)

set(BUNDLE_SRCS
	${RESROOT}/Info.plist
	${COMMON_RESROOT}/Assets.xcassets
	${COMMON_RESROOT}/abc.png
)

SET(EXECUTABLE_OUTPUT_PATH ${BIN_DIR})

link_libraries("-framework Foundation" "-framework UIKit" "-framework CoreGraphics" "-framework QuartzCore" "-framework CoreMotion" "-framework Metal" "-framework OpenGLES" "-framework OpenAL" "-framework AudioToolbox" "-framework AVFoundation")

add_executable(${PROJECTNAME} ${DIR_SRCS} ${BUNDLE_SRCS})

set_target_properties(
	${PROJECTNAME}
	PROPERTIES
	MACOSX_BUNDLE YES
	MACOSX_BUNDLE_INFO_PLIST "${RESROOT}/Info.plist"
	RESOURCE "${BUNDLE_SRCS}"
)
	
set_target_properties(
	${PROJECTNAME}
	PROPERTIES
	XCODE_ATTRIBUTE_ASSETCATALOG_COMPILER_APPICON_NAME "AppIcon"
	XCODE_ATTRIBUTE_ASSETCATALOG_COMPILER_LAUNCHIMAGE_NAME "LaunchImage"
	XCODE_ATTRIBUTE_CODE_SIGN_IDENTITY "iPhone Developer"
	XCODE_ATTRIBUTE_TARGETED_DEVICE_FAMILY "1"
	XCODE_ATTRIBUTE_CLANG_ENABLE_MODULES "YES"
	XCODE_ATTRIBUTE_DEVELOPMENT_TEAM "${IOS_TEAM}"
	XCODE_ATTRIBUTE_PRODUCT_BUNDLE_IDENTIFIER "${BUNDLE_IDENT}"
)
