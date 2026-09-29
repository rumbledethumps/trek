cmake_minimum_required(VERSION 3.21)

include(${CMAKE_CURRENT_LIST_DIR}/tools/rp6502.cmake)

project(trek BASIC)

add_executable(trek)
rp6502_asset(trek instructions.bas src/instructions.bas)
rp6502_asset(trek game.bas src/game.bas)
rp6502_basic(trek BASIC build-96e229e instructions.bas)
rp6502_web(trek EMULATOR tools/rp6502-web.zip CONFIG [[
    title: 'Super Star Trek',
    overlay: '',
    border: '1em',
    footer: 'Type a command, then press Enter. XXX resigns.',
]])

# The play test runs the ROM with no arguments, so autorun.bas starts it.
enable_testing()
if(CMAKE_HOST_SYSTEM_VERSION MATCHES "[Mm]icrosoft")
    set(emulator ${RP6502_TOOLS_DIR}/rp6502-emu.exe)
else()
    set(emulator ${RP6502_TOOLS_DIR}/rp6502-emu)
endif()
add_test(NAME play
    COMMAND ${emulator}
        --script ${CMAKE_CURRENT_SOURCE_DIR}/tests/play.txt
        --phi2=0 --seed 1
        ${CMAKE_CURRENT_BINARY_DIR}/trek.rp6502
)
set_tests_properties(play PROPERTIES TIMEOUT 120)
