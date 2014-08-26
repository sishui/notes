## 利用 NDK-STACK 来辅助分析堆栈追踪
  * 使用方法
<!-- lang:Shell -->
		adb logcat | $NDK/ndk-stack -sym $PROJECT_PATH/obj/local/armeabi

or

<!-- lang:Shell -->
		adb logcat > /tmp/log.txt
		$NDK/ndk-stack -sym $PROJECT_PATH/obj/local/armeabi -dump log.txt

   * 重要提示, ndk-stack tool的logcat输出需要有一个初始化行，一般情况如下
<!-- lang:Shell -->
		*** *** *** *** *** *** *** *** *** *** *** *** *** *** *** ***

   * 参考文档: $NDK_ROOT/docs/NDK-STACK.html 