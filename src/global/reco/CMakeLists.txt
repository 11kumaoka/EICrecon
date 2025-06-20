cmake_minimum_required(VERSION 3.16)

get_filename_component(PLUGIN_NAME ${CMAKE_CURRENT_LIST_DIR} NAME)

# Function creates ${PLUGIN_NAME}_plugin and ${PLUGIN_NAME}_library targets
# Setting default includes, libraries and installation paths
plugin_add(${PLUGIN_NAME} PLUGIN_USE_CC_ONLY)

# The macro grabs sources as *.cc *.cpp *.c and headers as *.h *.hh *.hpp Then
# correctly sets sources for ${_name}_plugin and ${_name}_library targets Adds
# headers to the correct installation directory
plugin_glob_all(${PLUGIN_NAME})

# Find dependencies
plugin_add_dd4hep(${PLUGIN_NAME})
plugin_add_cern_root(${PLUGIN_NAME})
plugin_add_event_model(${PLUGIN_NAME})

# The macro grabs sources as *.cc *.cpp *.c and headers as *.h *.hh *.hpp Then
# correctly sets sources for ${_name}_plugin and ${_name}_library targets Adds
# headers to the correct installation directory
plugin_glob_all(${PLUGIN_NAME})

# Add include directories (works same as target_include_directories)
# plugin_include_directories(${PLUGIN_NAME} SYSTEM PUBLIC ... )

# Add libraries (same as target_include_directories but for both plugin and
# library)
plugin_link_libraries(${PLUGIN_NAME} algorithms_digi_library
                      algorithms_tracking_library algorithms_reco_library)
if(USE_ONNX)
  plugin_link_libraries(${PLUGIN_NAME} algorithms_onnx_library)
endif()
