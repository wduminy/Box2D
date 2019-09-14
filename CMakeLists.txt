cmake_minimum_required(VERSION 3.8)
project (Box2D)
set (CMAKE_CXX_STANDARD 17) 
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17 -Wall")
set (CMAKE_CXX_FLAGS_RELEASE "-Ofast")

set(SOURCES
  Box2D/Collision/b2BroadPhase.cpp
  Box2D/Collision/b2CollideCircle.cpp
  Box2D/Collision/b2CollideEdge.cpp
  Box2D/Collision/b2CollidePolygon.cpp
  Box2D/Collision/b2Collision.cpp
  Box2D/Collision/b2Distance.cpp
  Box2D/Collision/b2DynamicTree.cpp
  Box2D/Collision/b2TimeOfImpact.cpp
  Box2D/Collision/Shapes/b2ChainShape.cpp
  Box2D/Collision/Shapes/b2CircleShape.cpp
  Box2D/Collision/Shapes/b2EdgeShape.cpp
  Box2D/Collision/Shapes/b2PolygonShape.cpp
  Box2D/Common/b2BlockAllocator.cpp
  Box2D/Common/b2Draw.cpp
  Box2D/Common/b2Math.cpp
  Box2D/Common/b2Settings.cpp
  Box2D/Common/b2StackAllocator.cpp
  Box2D/Common/b2Timer.cpp
  Box2D/Dynamics/Contacts/b2ChainAndCircleContact.cpp
  Box2D/Dynamics/Contacts/b2ChainAndPolygonContact.cpp
  Box2D/Dynamics/Contacts/b2CircleContact.cpp
  Box2D/Dynamics/Contacts/b2Contact.cpp
  Box2D/Dynamics/Contacts/b2ContactSolver.cpp
  Box2D/Dynamics/Contacts/b2EdgeAndCircleContact.cpp
  Box2D/Dynamics/Contacts/b2EdgeAndPolygonContact.cpp
  Box2D/Dynamics/Contacts/b2PolygonAndCircleContact.cpp
  Box2D/Dynamics/Contacts/b2PolygonContact.cpp
  Box2D/Dynamics/Joints/b2DistanceJoint.cpp
  Box2D/Dynamics/Joints/b2FrictionJoint.cpp
  Box2D/Dynamics/Joints/b2GearJoint.cpp
  Box2D/Dynamics/Joints/b2Joint.cpp
  Box2D/Dynamics/Joints/b2MotorJoint.cpp
  Box2D/Dynamics/Joints/b2MouseJoint.cpp
  Box2D/Dynamics/Joints/b2PrismaticJoint.cpp
  Box2D/Dynamics/Joints/b2PulleyJoint.cpp
  Box2D/Dynamics/Joints/b2RevoluteJoint.cpp
  Box2D/Dynamics/Joints/b2RopeJoint.cpp
  Box2D/Dynamics/Joints/b2WeldJoint.cpp
  Box2D/Dynamics/Joints/b2WheelJoint.cpp
  Box2D/Dynamics/b2Body.cpp
  Box2D/Dynamics/b2ContactManager.cpp
  Box2D/Dynamics/b2Fixture.cpp
  Box2D/Dynamics/b2Island.cpp
  Box2D/Dynamics/b2World.cpp
  Box2D/Dynamics/b2WorldCallbacks.cpp
  Box2D/Rope/b2Rope.cpp
)

add_library(box2d STATIC ${SOURCES})
target_include_directories( box2d PUBLIC .)


add_executable(hello_app HelloWorld/HelloWorld.cpp)
target_include_directories(hello_app PUBLIC .)
target_link_libraries(hello_app box2d)

set(TEST_SOURCES
Testbed/Framework//Test.cpp
Testbed/Framework//Main.cpp
Testbed/Framework//DebugDraw.cpp
Testbed/Tests/TestEntries.cpp
Testbed/glfw/context.c
Testbed/glfw/init.c
Testbed/glfw/input.c
Testbed/glfw/monitor.c
Testbed/glfw/vulkan.c
Testbed/glfw/window.c
Testbed/imgui/imgui_impl_glfw_gl3.cpp
Testbed/imgui/imgui_demo.cpp
Testbed/imgui/imgui_draw.cpp
Testbed/glfw/cocoa_init.m
Testbed/glfw/cocoa_joystick.m
Testbed/glfw/cocoa_monitor.m
Testbed/glfw/cocoa_window.m
Testbed/glfw/cocoa_time.c
Testbed/glfw/posix_tls.c
Testbed/glfw/nsgl_context.m
Testbed/glfw/egl_context.c
Testbed/imgui/imgui.cpp
Testbed/imgui/imgui_impl_glfw_gl3.cpp
Testbed/imgui/imgui_demo.cpp
Testbed/imgui/imgui_draw.cpp
)

set(CMAKE_FIND_FRAMEWORK FIRST)
find_library(OpenGL REQUIRED)
find_library(Cocoa REQUIRED)
find_library(IOKit REQUIRED)
find_library(CoreFoundation REQUIRED)
find_library(CoreVideo REQUIRED)

set_source_files_properties(*.m PROPERTIES LANGUAGE CXX )
add_executable(test_box2d ${TEST_SOURCES})
target_link_libraries(test_box2d 
 box2d 
 "-framework OpenGL"
 "-framework Cocoa"
 "-framework IOKit"
 "-framework CoreFoundation"
 "-framework CoreVideo"
 )

 configure_file(Testbed/Data/DroidSans.ttf Data/DroidSans.ttf COPYONLY)
 target_include_directories(test_box2d PUBLIC 
	${OPENGL_INCLUDE_DIR} 
	${COCOA_INCLUDE_DIR} 
	${IOKIT_INCLUDE_DIR} 
	${COREFOUNDATION_INCLUDE_DIR} 
	${COREVIDEO_INCLUDE_DIR} 
)

