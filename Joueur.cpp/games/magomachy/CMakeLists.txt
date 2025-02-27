##########################
# IMPLEMENTATION DETAILS #
# DO NOT EDIT THIS FILE  #
##########################

file(READ ${CMAKE_CURRENT_SOURCE_DIR}/additional_files.txt extras)

add_custom_target(Magomachy_additional ALL
    COMMAND ${CMAKE_COMMAND} -E touch ${CMAKE_CURRENT_SOURCE_DIR}/CMakeLists.txt
    DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/additional_files.txt)

string(REPLACE "\n" ";" extras ${extras})

foreach(file IN ITEMS ${extras})
    string(SUBSTRING ${file} 0 1 check)
    if(NOT ${check} STREQUAL "#")
        if(NOT EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/${file})
            message(FATAL_ERROR "Could not find additional file \"${file}\"!")
        endif(NOT EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/${file})
        list(APPEND to_add ${CMAKE_CURRENT_SOURCE_DIR}/${file})
        message(STATUS ${file})
    endif(NOT ${check} STREQUAL "#")
endforeach(file)


add_dependencies(dependencies Magomachy_additional)

set(FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/ai.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/ai.hpp
    ${CMAKE_CURRENT_SOURCE_DIR}/impl/ai_impl.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/impl/magomachy.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/impl/magomachy.hpp
    ${CMAKE_CURRENT_SOURCE_DIR}/impl/magomachy_fwd.hpp
    ${CMAKE_CURRENT_SOURCE_DIR}/game_object.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/game_object.hpp
    ${CMAKE_CURRENT_SOURCE_DIR}/impl/game_object_impl.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/item.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/item.hpp
    ${CMAKE_CURRENT_SOURCE_DIR}/impl/item_impl.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/player.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/player.hpp
    ${CMAKE_CURRENT_SOURCE_DIR}/impl/player_impl.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/tile.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/tile.hpp
    ${CMAKE_CURRENT_SOURCE_DIR}/impl/tile_impl.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/wizard.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/wizard.hpp
    ${CMAKE_CURRENT_SOURCE_DIR}/impl/wizard_impl.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/game.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/game.hpp
    ${CMAKE_CURRENT_SOURCE_DIR}/impl/game_impl.cpp
    ${to_add}
    PARENT_SCOPE)
