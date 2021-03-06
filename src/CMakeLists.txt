add_subdirectory(libopenrazer)

if(ENABLE_EXPERIMENTAL)
    add_definitions(-DENABLE_EXPERIMENTAL)
    message("razergenie: Experimental features enabled.")
else()
    message("razergenie: Experimental features disabled.")
endif()

if(INCLUDE_MATRIX_DISCOVERY)
    add_definitions(-DINCLUDE_MATRIX_DISCOVERY)
    message("razergenie: Matrix discovery feature included.")
else()
    message("razergenie: Matrix discovery feature not included.")
endif()

set(razergenie_SRCS main.cpp
                    razergenie.cpp
                    razerimagedownloader.cpp
                    razerdevicewidget.cpp
                    devicelistwidget.cpp
                    util.cpp
                    customeditor/customeditor.cpp
                    customeditor/matrixpushbutton.cpp
                    preferences/preferences.cpp
                    )

QT5_WRAP_UI(razergenie_SRCS ../ui/razergenie.ui)

configure_file(config.h.in ${CMAKE_CURRENT_BINARY_DIR}/config.h)

add_executable(razergenie ${razergenie_SRCS})
target_link_libraries(razergenie openrazer Qt5::Widgets Qt5::DBus Qt5::Network)

install(TARGETS razergenie DESTINATION ${CMAKE_INSTALL_BINDIR})
