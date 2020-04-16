cmake_minimum_required(VERSION 3.15)

project(PluginVal VERSION 0.2.4)

add_subdirectory(modules/JUCE)

juce_add_gui_app(PluginVal
    BUNDLE_ID                       com.juce.pluginhost
    COMPANY_NAME                    Tracktion
    ICON_BIG                        "${CMAKE_CURRENT_SOURCE_DIR}/Source/binarydata/icon.png")

juce_generate_juce_header(PluginVal)

target_compile_features(PluginVal PRIVATE cxx_std_14)

set_target_properties(PluginVal PROPERTIES
    C_VISIBILITY_PRESET hidden
    CXX_VISIBILITY_PRESET hidden)

target_sources(PluginVal PRIVATE
    Source/CommandLine.cpp
    Source/CrashHandler.cpp
    Source/Main.cpp
    Source/MainComponent.cpp
    Source/PluginTests.cpp
    Source/Tests/BasicTests.cpp
    Source/Tests/BusTests.cpp
    Source/Tests/ParameterFuzzTests.cpp
    Source/Validator.cpp)

target_compile_definitions(PluginVal PRIVATE
    JUCE_PLUGINHOST_AU=1
    JUCE_PLUGINHOST_LADSPA=1
    JUCE_PLUGINHOST_VST3=1
    JUCE_USE_CURL=0
    JUCE_WEB_BROWSER=0)

target_link_libraries(PluginVal PRIVATE
    juce::juce_audio_devices
    juce::juce_audio_processors
    juce::juce_audio_utils)
