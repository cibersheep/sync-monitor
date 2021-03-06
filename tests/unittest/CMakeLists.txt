macro(declare_test TESTNAME)
    add_executable(${TESTNAME}
                   ${ARGN})
    qt5_use_modules(${TESTNAME} Core Test Contacts)

    target_link_libraries(${TESTNAME}
                          ${ACCOUNTS_LIBRARIES}
                          synq-lib
                          gmock
    )

    add_test(${TESTNAME} ${TESTNAME})
endmacro()

include_directories(
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}
    ${ACCOUNTS_INCLUDE_DIRS}
    ${syncevolution-qt_SOURCE_DIR}
    ${gmock_SOURCE_DIR}/gtest/include/
)

declare_test(sync-queue-test
             sync-queue-test.cpp
             sync-account-mock.h
)

declare_test(eds-helper-test
             eds-helper-test.cpp
             eds-helper-mock.h
)

declare_test(syncevolution-output-parser
             syncevolution-output-parser.cpp
             ${CMAKE_SOURCE_DIR}/3rd_party/syncevolution-qt/dbustypes.cpp)
