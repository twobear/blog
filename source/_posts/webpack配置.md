# webpack 配置常用设置

## 项目中配制项目目录别名
自己的项目里想设置，比较简短的缩写路径，比如：
```
      config ={
        ...
          resolve: {
            extensions: [".js", ".ts", ".json"],
            alias:{
              "@src":path.resolve("src"),
              "@component":path.resolve("src/component"),
              "@lib":path.resolve("libs"),
              "@utils":path.resolve("src/utils"),
            },
        },
      }
```      
这里设置完成后，编辑器检查会提示你不存在这个路径，这个时候我们就需要设置项目中的另外一个文件了，jsconfig.json/tsconfig.json
把里边的 compilerOptions 的path一同设置：
```
{
...
  "compilerOptions": {
    "paths":{
      "@/*": ["src/*"],
      "@lib/*":["libs/*"]
    }
  },
}

```

重启目devserver
