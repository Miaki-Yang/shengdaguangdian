file(GLOB_RECURSE SOURCES ./*.c)

set(incdirs "."
            "lvgl"
            "lvgl/src")

idf_component_register(SRCS ${SOURCES}
                       INCLUDE_DIRS "${incdirs}"
                       REQUIRES mqtt mbedtls json)

target_compile_definitions(${COMPONENT_LIB} INTERFACE LV_CONF_INCLUDE_SIMPLE=1)
add_prebuilt_library(liblvgl "liblvgl.a" REQUIRES mqtt mbedtls json spi_flash spiffs)
target_link_libraries(${COMPONENT_LIB} INTERFACE liblvgl)
