
project(kayak_logger_esp8266)

include(${ARDUINO_CMAKE_DIR}/esp8266/paths.cmake)
include(${ARDUINO_CMAKE_DIR}/esp8266/tools.cmake)
include(${ARDUINO_CMAKE_DIR}/esp8266/defs.cmake)
include(${ARDUINO_CMAKE_DIR}/esp8266/core.cmake)
include(${ARDUINO_CMAKE_DIR}/esp8266/deploy.cmake)

set(sources
    ${SRC_DIR}/Loop.cpp
    ${SRC_DIR}/Setup.cpp
    ${SRC_DIR}/GpsReport.cpp
    ${SRC_DIR}/ElementQueue.cpp
    ${SRC_DIR}/AverageSpeed.cpp
    ${SRC_DIR}/Distance.cpp
    ${SRC_DIR}/LogElement.cpp
    ${SRC_DIR}/StatusIndicator.cpp
    ${SRC_DIR}/Logger.cpp
    ${SRC_DIR}/Components.cpp
    ${SRC_DIR}/TiltReport.cpp
    ${ACCELEROMETER_DIR}/ADXL345.cpp
#    ${ARDUINO_LCD_SRC}/LiquidCrystal.cpp
    ${IIC_LCD_SRC}/LiquidCrystal_I2C.cpp
#    ${ARDUINO_WIRE_SRC}/Wire.cpp
#    ${ARDUINO_WIRE_SRC}/utility/twi.c
    ${SDFAT_ESP8266_DIR}
    ${GPS_DIR}/TinyGPS.cpp
    ${SPI_ESP8266_DIR}/SPI.cpp
    ${SDFAT_ESP8266_DIR}/File.cpp
    ${SDFAT_ESP8266_DIR}/SD.cpp
    ${SDFAT_ESP8266_DIR}/utility/Sd2Card.cpp
    ${SDFAT_ESP8266_DIR}/utility/SdFile.cpp
    ${SDFAT_ESP8266_DIR}/utility/SdVolume.cpp
)

add_executable(${PROJECT_NAME} ${sources})
target_link_libraries(${PROJECT_NAME} esp8266_core)
target_compile_options(
    ${PROJECT_NAME} PRIVATE
    ${compiler_set_2}
    -DESP8266_BUILD_ERRORS
)

target_include_directories(
    ${PROJECT_NAME} PRIVATE
    ${SRC_DIR}
    ${GPS_DIR}
    ${SDFAT_ESP8266_DIR}
    ${SPI_ESP8266_DIR}
    ${WIRE_ESP8266_DIR}
    ${IIC_LCD_SRC}
    ${ACCELEROMETER_DIR}
)

elf_to_bin(${PROJECT_NAME})
upload(${PROJECT_NAME} elf_to_bin_${PROJECT_NAME})