add_custom_target(
	bundle.hh
	COMMAND cp -rf app ${CMAKE_CURRENT_BINARY_DIR}
	COMMAND cp $<TARGET_FILE:popcalc> ${CMAKE_CURRENT_BINARY_DIR}/app/Contents/MacOS/popcalc
	COMMAND python3 "${PROJECT_SOURCE_DIR}/embed.py" "${CMAKE_CURRENT_BINARY_DIR}/app" > ${CMAKE_CURRENT_BINARY_DIR}/bundle.hh
	DEPENDS popcalc
	WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
)

add_executable(popcalc main.c getroot.c)

target_compile_options(popcalc PUBLIC
	-DCURRENT_DIR="${CMAKE_CURRENT_SOURCE_DIR}"
)