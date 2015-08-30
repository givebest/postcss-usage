# PostCSS一种更优雅、更简单的书写CSS方式

[Sass](http://sass-lang.com)团队创建了[Compass](http://compass-style.org)大大提升CSSer的工作效率,你无需考虑各种浏览器前缀兼,只需要按官方文档的书写方式去写,会得到加上浏览器前缀的代码,如下:

	.row {
	  @include display-flex;
	}

会得到如下代码:

	.row {
	  display: -webkit-flex; 
	  display: flex;
	}

但是, 做为一个长期用原生CSS书写方式的CSSer,不太习惯去官方查文档,再以`@include`方式书写。

那么问题来了,我只能放弃高效率方式么?
其实不然, [Autoprefixer](https://github.com/postcss/autoprefixer)能够帮助你。
其实, [Autoprefixer](https://github.com/postcss/autoprefixer)也仅仅是[PostCSS](https://github.com/postcss/postcss)其一个最出名的插件。
来吧, 来看张图:

---
![](http://images2015.cnblogs.com/blog/23444/201508/23444-20150830170253469-1653052336.png)
---

这样,以一种原生CSS的书写方式, 然后还可以帮你解决浏览器前缀、IE兼容、以下一代CSS书写方式兼容现在浏览器, 是不是很酷?        
>哦, 其实应该说更简单、更优雅, 不用查文档, 不用`@include`。       
>这个就是Twitter推出的PostCSS, 据说Google、阿里、Shopify, Twitter就不用说了, 他们都在用PostCSS。      

上图有用到的PostCSS插件有:

[CSSNext](https://github.com/cssnext/cssnext), 可以看到下一代CSS开始支持`变量`了,这是否意味着'Sass'、'Less'不再重要了? 更多方法法可访问:[http://cssnext.io/features/](http://cssnext.io/features/)    
[Autoprefixer](https://github.com/postcss/autoprefixer), 知名度很高的PostCSS插件,支持`Gulp`、`Webpack`、`Grunt`、`Compass`等,了解更多可访问: [https://github.com/postcss/autoprefixer](https://github.com/postcss/autoprefixer)    
[CSS Grace](https://github.com/cssdream/cssgrace), 国内大神写的实现了大部分常用的 `IE Hack` 的插件, 中文文档: [https://github.com/cssdream/cssgrace/blob/master/README-zh.md](https://github.com/cssdream/cssgrace/blob/master/README-zh.md)    

当然还有更多PostCSS插件可访问: [http://postcss.parts](http://postcss.parts)

好了,下面看下PostCSS一些基本使用方法吧:

## 准备

>构建工具为[Gulp](https://github.com/gulpjs/gulp)       
>基于[PostCSS](https://github.com/postcss/postcss)       
>PostCSS插件 [CSSNext](https://github.com/cssnext/cssnext) 用下一代CSS书写方式兼容现在浏览器       
>PostCSS插件 [Autoprefixer](https://github.com/postcss/autoprefixer) 为CSS补全浏览器前缀       
>PostCSS插件 [CSS Grace](https://github.com/cssdream/cssgrace) 让CSS兼容旧版IE         

## package.json

	{
	  "name": "postcss usage",
	  "version": "1.0.0",
	  "description": "postcss cssnext",
	  "main": "gulpfile.js",
	  "dependencies": {
	    "autoprefixer": "^5.2.0",
	    "autoprefixer-core": "^5.2.1",
	    "cssgrace": "^2.0.2",
	    "gulp": "^3.9.0",
	    "gulp-less": "^3.0.3"
	  },
	  "devDependencies": {
	    "autoprefixer": "^5.2.0",
	    "autoprefixer-core": "^5.2.1",
	    "cssgrace": "^2.0.2",
	    "cssnext": "^1.8.4",
	    "gulp-postcss": "^6.0.0",
	    "postcss": "^4.1.16"
	  },
	  "scripts": {
	    "test": "echo \"Error: no test specified\" && exit 1"
	  },
	  "keywords": [
	    "postcss",
	    "gulp"
	  ],
	  "author": "givebest",
	  "license": "ISC"
	}

## gulpfile.js

	var gulp = require('gulp');
	var postcss = require('gulp-postcss');
	var autoprefixer = require('autoprefixer');
	var cssgrace  = require('cssgrace');
	var cssnext  = require('cssnext');
	
	gulp.task('css', function () {
	    var processors = [
	        autoprefixer({browsers: ['last 3 version'],
	        	cascade: false,
	        	remove: false
	    	}),
	        cssnext(),
	        cssgrace
	    ];
	    return gulp.src('./src/css/*.css')
	        .pipe(postcss(processors))
	        .pipe(gulp.dest('./dist'));
	});
	gulp.task('watch', function(){
		gulp.watch('./src/css/*.css', ['css']);
	});
	
	gulp.task('default', ['watch', 'css']);

## 安装

	npm install	

## 使用

	gulp



>详细项目地址在: [https://coding.net/u/givebest/p/postcss-usage/git](https://coding.net/u/givebest/p/postcss-usage/git)

	