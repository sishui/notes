### xcode
每次编译，都需要清理，不然不更新lua脚本的问题

解决办法：
工程设置里->Build Phases-> 新建 Run Script
<!-- lang:Shell -->
	_TARGET_BUILD_CONTENTS_PATH=$TARGET_BUILD_DIR/$CONTENTS_FOLDER_PATH
	echo _TARGET_BUILD_CONTENTS_PATH: $_TARGET_BUILD_CONTENTS_PATH
	echo PWD: $PWD

	echo Cleaning $_TARGET_BUILD_CONTENTS_PATH/

	rm -fr $_TARGET_BUILD_CONTENTS_PATH/res/*
	rm -fr $_TARGET_BUILD_CONTENTS_PATH/scripts/*

	mkdir -p $_TARGET_BUILD_CONTENTS_PATH/res/
	mkdir -p $_TARGET_BUILD_CONTENTS_PATH/scripts/

	cp -RLp $PWD/../res/* $_TARGET_BUILD_CONTENTS_PATH/res/
	cp -RLp $PWD/../scripts/* $_TARGET_BUILD_CONTENTS_PATH/scripts/

	find "${_TARGET_BUILD_CONTENTS_PATH}/res" \( -name ".svn" -o -name ".DS_Store" \) -exec  rm -rf {} \; -prune
	find "${_TARGET_BUILD_CONTENTS_PATH}/scripts" \( -name ".svn" -o -name ".DS_Store" \) -exec rm -rf {} \; -prune
