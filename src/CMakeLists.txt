
find_package(Wireshark REQUIRED)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH};${Wireshark_DIR};${CMAKE_SOURCE_DIR}/cmake/modules)
message(STATUS "CMAKE_MODULE_PATH: ${CMAKE_MODULE_PATH}")

# Wireshark_INCLUDE_DIR

include(UseMakePluginReg)
include(WiresharkPlugin)

# # Plugin name and version info (major minor micro extra)
set_module_info(foo 0 0 4 0)

set(DISSECTOR_SRC
	packet-foo.c
)

set(PLUGIN_FILES
	plugin.c
	${DISSECTOR_SRC}
)

set_source_files_properties(
	${PLUGIN_FILES}
	PROPERTIES
	COMPILE_FLAGS "${WERROR_COMMON_FLAGS}"
)

register_plugin_files(plugin.c
	plugin
	${DISSECTOR_SRC}
)

add_wireshark_plugin_library(foo)

target_link_libraries(foo epan)

install(TARGETS foo
		LIBRARY DESTINATION plugins)