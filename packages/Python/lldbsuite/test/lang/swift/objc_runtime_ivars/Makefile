LEVEL = ../../../make

include $(LEVEL)/Makefile.rules

framework_nodbg: framework
	rm -rf aTestFramework.framework.dSYM

framework: cleanup
	xcodebuild -configuration Release -project framework/aTestFramework/aTestFramework.xcodeproj CONFIGURATION_BUILD_DIR=$(shell pwd)
	cp module.map aTestFramework.framework/

exec_impl:
	$(SWIFTC) $(SWIFT_MODULE_CACHE_FLAGS) -g -Onone -o main main.swift -framework aTestFramework -framework Cocoa -sdk "$(SWIFTSDKROOT)" -F "$(shell pwd)"

ifneq "$(CODESIGN)" ""
	$(CODESIGN) -s - main
endif

exec: framework exec_impl

exec_nodbg: framework_nodbg exec_impl

cleanup:
	rm -rf main aTestFramework.framework aTestFramework.framework.dSYM main.dSYM
	rm -rf framework/aTestFramework/build
	rm -rf framework/aTestFramework/intermediates

