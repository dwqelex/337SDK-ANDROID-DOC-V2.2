Email形式客诉实现方法
---------------------

基础的面板是一个透明背景的Dialog组件，组件中添加的View就是设计好的带个Webview和有控制按钮的一个布局。

Dialog初始化时Webview直接去加载一个固定的指向默认FAQ的页面URL（一个简单的网页即可），加载完毕之前可以先放一个进度条保证体验良好。

其他的控制按钮，如关闭、发送Email等功能直接加Listener即可。

点击发送Email时，可以先获取一些设备信息和游戏信息，比如系统版本、型号，游戏服、角色名等，拼出一个格式比较好的文本作为邮件的默认文本。

发送邮件的方法: ::

	Intent intent = new Intent(Intent.ACTION_SENDTO,Uri.parse(MailTo.MAILTO_SCHEME));
	intent.putExtra(Intent.EXTRA_SUBJECT, subject);//主题
	intent.putExtra(Intent.EXTRA_TEXT, text);//正文
	intent.putExtra(Intent.EXTRA_EMAIL, to);//收件人
	startActivity(Intent.createChooser(intent, "发送邮件"));

填好收件人、主题、和之前拼好的默认文本，就可以直接发送邮件了。

系统会自动提示玩家选择相应的邮件客户端去发送。剩下的事就可以不用管了，发送完邮件后会自动返回游戏。