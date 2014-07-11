title: hexo2.7.1
date: 2014-07-12 02:11:06
category: hexo
tags: hexo 

---

今天升级了2.7.1，结果跑不起来了。。跑出来的主页直接是一些代码，原来render模块被剥离了，需要独立安装

	npm install hexo-renderer-ejs --save
	npm install hexo-renderer-stylus --save
	npm install hexo-renderer-marked --save



##参考
《升级hexo》-－黄云坤
>http://www.huangyunkun.com/2014/06/18/update-hexo/