cmake_minimum_required(VERSION 3.21)

include(${CMAKE_CURRENT_LIST_DIR}/tools/rp6502.cmake)

project(trek BASIC)

add_executable(trek)
rp6502_asset(trek help src/help.txt)
rp6502_asset(trek instructions.bas src/instructions.bas)
rp6502_asset(trek game.bas src/game.bas)
rp6502_basic(trek BASIC build-96e229e instructions.bas)
rp6502_web(trek CONFIG [[
    title: 'Super Star Trek',
    border: '1em',
    overlay: '',
    footer: 'Type a command, then press Enter. XXX resigns.',
]])

# The play test runs the ROM with no arguments, so autorun.bas starts it.
enable_testing()
find_package(Python3 REQUIRED COMPONENTS Interpreter)
add_test(NAME play
    COMMAND ${Python3_EXECUTABLE} ${RP6502_TOOLS_DIR}/rp6502.py
        -c ${CMAKE_CURRENT_SOURCE_DIR}/.rp6502 execute
        --script ${CMAKE_CURRENT_SOURCE_DIR}/tests/play.txt --seed 1
        ${CMAKE_CURRENT_BINARY_DIR}/trek.rp6502
)
set_tests_properties(play PROPERTIES TIMEOUT 120)
