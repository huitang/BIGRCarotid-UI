PROJECT(medialness)

ADD_EXECUTABLE(medialness
               medialness.cxx )
     
TARGET_LINK_LIBRARIES(medialness  ${ITK_LIBRARIES})

