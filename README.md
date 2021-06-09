## lerna 基本命令
### lerna初始化
+ `lerna init` 初始化项目
### 创建package
+ `lerna create packageName`
  + 注意这个包的名称一般是@organizationsName/packagename，文件夹名称不一定是这种格式 但是package.json中的name要是这种格式，不然可能发不上去包
  + 创建组织organizations，在npm点击头像，packages，左侧organizations点击创建一个新的组织
### 安装依赖
+ `lerna add packageName` 不指定参数会在packages下面的所有包都安装依赖
  + `lerna add packageName packages/xx` 给packages下面的指定目录安装依赖
### 清空依赖
+ `lerna clean` 不指定参数 就是清除packages下面所有项目的依赖（删除node_modules），但是不会清除package.json中的依赖项
### 重新安装依赖
+ `lerna bootstrap`
### 链接packages中的包的相互依赖
+ `lerna link` 实现packages中的包的相互依赖的软链接
### 执行脚本
+ `lerna exec -- scripts` 在packages下面的每个包中执行指定脚本
  + `lerna exec --scope packageName -- scripts` 在packages下指定包（packageName是包的全名而不是路径）执行指定脚本
### 执行npm命令
+ `lerna run npmScript` 执行npm脚本，package.json中scripts里面的命令
  + `lerna run --scope packageName npmScript`


## lerna发布相关的命令
### 更新版本号
+ `lerna version` 需要发布后才能使用
### 查看变更信息
+ `lerna changed`
### 查看当前文件信息和上次commit之间的变更
+ `lerna diff`
### 发布
+ `lerna publish`

### 发布时的一些小问题
1. `lerna ERR! E402 You must sign up for private packages`， 因为我们packages下面的包在发布的时候，默认是以分组下的私有包发布
  + 解决方案
    1. 执行`lerna publish`的时候添加`--access pulic`属性
    2. 在packages下对应包的package.json中添加
        ```
          "publishConfig": {
            "access": "public"
          }
        ```
2. `lerna WARN ENOLICENSE One way to fix this is to add a LICENSE.md file to the root of this repository.`
  + 在项目根目录下添加LICENSE.md文件
