idf_component_register(SRCS "power_save.c"
                       INCLUDE_DIRS "." REQUIRES )
target_compile_options(${COMPONENT_LIB} PRIVATE "-Wno-format")
