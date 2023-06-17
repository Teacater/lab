cmake_minimum_required(VERSION 3.21)
project(CMakeSFMLProject LANGUAGES CXX)

include(FetchContent)
FetchContent_Declare(SFML
    GIT_REPOSITORY https://github.com/SFML/SFML.git
    GIT_TAG 2.6.x)
FetchContent_MakeAvailable(SFML)

add_executable(CMakeSFMLProject src/main.cpp src/GameObject.h src/Game.h src/GameObjectFactory.h src/Portal.h src/Empty.h src/Enemy.h src/Chest.h src/Cell.h src/Board.h src/Menu.h src/Player.h src/Command.h src/PlayerMoveCommand.h src/CommandInvoker.h src/Portal.cpp src/Empty.cpp src/Enemy.cpp src/Chest.cpp src/Wall.cpp src/Wall.h)
target_link_libraries(CMakeSFMLProject PRIVATE sfml-graphics)
target_compile_features(CMakeSFMLProject PRIVATE cxx_std_17)
if (WIN32 AND BUILD_SHARED_LIBS)
    add_custom_command(TARGET CMakeSFMLProject POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_RUNTIME_DLLS:CMakeSFMLProject> $<TARGET_FILE_DIR:CMakeSFMLProject> COMMAND_EXPAND_LISTS)
endif()

install(TARGETS CMakeSFMLProject)
