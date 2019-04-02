---
title: gulp无法生成文件
intro: '1.模糊查找匹配文件，路径不对题导致'
comments: false
date: 2019-02-14 16:36:23
tags: js , gulp
---



结论：
  1.模糊查找匹配文件，路径不对题导致（简单测试就是把，模糊查找的相对路劲换为文件精度的相对路径进行查看）
  2.其他待补充

项目中有使用gulp生成文件时候，有时需要批量查找某类型文件进行编辑修改。目录为`src/style/`,代码如下：
    function compile() {
        return src('src/style/*.scss')
            .pipe(sass.sync())
            .pipe(autoprefixer({
                browsers: ['ie > 9', 'last 2 versions'],
                cascade: false
            }))
            // .pipe(cssmin())
            .pipe(dest('lib'));
    }
    
    
 如果`gulpfile.js`放在根目录那么感觉没什么问题，但是如果`gulpfile.js`和你即将编译的文件分处不同文件夹，那么问题就暴露出来了。
 gulp执行的时候读取的路径是`gulpfile.js`所在的路径，所以你目标编译的文件路径，也应该相对于`gulpfile.js`而言。
  
 比如我的 `gulpfile.js` 文件放在 `build/` 文件夹里,目标编译的css为`src/style/`应该修改为：
 
    const projectPath = path.resolve(__dirname, '../');
    const basePath = path.resolve(__dirname, '../src/style');
    function compile() {
        return src(basePath+'/*.scss')
            .pipe(sass.sync())
            .pipe(autoprefixer({
                browsers: ['ie > 9', 'last 2 versions'],
                cascade: false
            }))
            // .pipe(cssmin())
            .pipe(dest(projectPath+'/lib'));
    }
    
  gulp 匹配不到对应文件没有报错，这个查起来比较麻烦，很容易忽略。
