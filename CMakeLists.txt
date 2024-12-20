CMAKE_MINIMUM_REQUIRED(VERSION 3.15)

PROJECT(ALGOMANCER
        VERSION 1.0
        DESCRIPTION "A Modular Data Structures Library in C"
        LANGUAGES C)

# Set C standard
SET(CMAKE_C_STANDARD 99)
SET(CMAKE_C_STANDARD_REQUIRED ON)

# Options for enabling/disabling modules
OPTION(BUILD_ARRAYS             "Build Arrays Module"             ON)
OPTION(BUILD_GRAPH              "Build Graph Module"              ON)
OPTION(BUILD_HASHTABLE          "Build Hashtable Module"          ON)
OPTION(BUILD_LINKEDLIST         "Build LinkedList Module"         ON)
OPTION(BUILD_PRIORITY_QUEUE     "Build Priority Queue Module"     ON)
OPTION(BUILD_QUEUE              "Build Queue Module"              ON)
OPTION(BUILD_STACK              "Build Stack Module"              ON)
OPTION(BUILD_TREES              "Build Trees Module"              ON)

# Add common utilities
ADD_SUBDIRECTORY(COMMON)

# Array of modules
SET(MODULES
    BUILD_ARRAYS
    BUILD_GRAPH
    BUILD_HASHTABLE
    BUILD_LINKEDLIST
    BUILD_PRIORITY_QUEUE
    BUILD_QUEUE
    BUILD_STACK
    BUILD_TREES
)

# Add enabled modules
FOREACH(MODULE ${MODULES})
    IF(${MODULE})
        STRING(REPLACE "BUILD_" "" MODULE_NAME ${MODULE})
        STRING(TOLOWER ${MODULE_NAME} MODULE_DIR)
        ADD_SUBDIRECTORY(${MODULE_DIR})
    ENDIF()
ENDFOREACH()

# Warn if no modules are enabled
IF(NOT (BUILD_ARRAYS OR BUILD_GRAPH OR BUILD_HASHTABLE OR BUILD_LINKEDLIST OR 
        BUILD_PRIORITY_QUEUE OR BUILD_QUEUE OR BUILD_STACK OR BUILD_TREES))
    MESSAGE(WARNING "No modules are enabled. Set BUILD_* options to ON to include specific modules.")
ENDIF()
