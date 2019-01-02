# 前端代码规范（Beta）
## 一、命名方式
### 1、js命名方式：语义化
* 函数、变量：小驼峰式 let tableTitle = ‘LoginTable'
* 常量：全部大写 const MAX_COUNT = 10;
* 类 构造函数：首字母大写，大驼峰式命名


#### 例如：
```javascript
class Person{
    public name : string;
    constructor(name){
         [this.name](this.name)  = name;
    }
}
const person = new Person ('mevyn');
```
* 公共属性和方法：跟变量和函数的命名一样。
* 私有属性和方法：前缀为 _（下划线），后面跟公共属性和方法一样的命名方式。

### 2、 css命名方式：语义化
* 缩进与换行：[强制] 使用 4个空格做为一个缩进层级，不允许使用 2个空格 或 tab字符。
* class 必须单词全字母小写，单词间以 - 分隔  block-element 
* Class 必须代表相应模块或部件的内容或功能，不得以样式信息进行命名
* [建议] 选择器的嵌套层级应不大于 3 级，位置靠后的限定条件应尽可能精确。


## 二、注释
### 1、单行注释
```javascript
// 这个函数的执行条件，执行结果大概说明
dosomthing()
```

### 2、多行注释
```javascript
/*
* xxxx  描述较多的时候可以使用多行注释
* xxxx
*/
dosomthing();
```

### 3、函数（方法）注释
```javascript
/**
 * 函数功能简述
 *
 * 具体描述一些细节
 *
 * @param    {string}  address     地址
 * @param    {array}   com         商品数组
 * @param    {string}  pay_status  支付方式
 * @returns  void
 *
 * @date     2014-04-12
 * @author   QETHAN< [qinbinyang@zuijiao.net](mailto:qinbinyang@zuijiao.net) >
 */
```

## 三、git规范
### 1、分支
* 命名：
master: master 分支就叫master 分支，线上环境正在使用的。
test: test分支就供测试环境使用的分支。

### 2、Commit标识规范
* 用于说明 commit 的类别，只允许使用下面7个标识。
1. feat：新功能（feature）
2. fix：修补bug
3. docs：文档（documentation）
4. Style： 格式（不影响代码运行的变动）
5. Refactor：重构（即不是新增功能，也不是修改bug的代码变动）
6. Test：增加测试
7. Chore：构建过程或辅助工具的变动

## 四、VScode 配置 SonarQube 进行代码扫描
### 1、下载[SonarQube](https://www.sonarqube.org/downloads/)及[SonarQube Scanner](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner/)并解压

- 注意： SonarQube下载 LTS版本， 解压后的文件建议存放在固定位置（以免误删）

### 2、配置环境变量及自定义命令

-  **将SonarQube Scanner目录中的bin文件夹添加进环境变量中**

  - 打开~/.bash_profile, 如果没有新建一个

    ```javascript
    export PATH="/Users/sunzitong/Documents/sonar-scanner-3.2.0.1227-macosx/bin:$PATH"
    PATH=$PATH

    // 改成你自己存放位置的地址
    ```

- **新建一个shell并编辑**

   ```javascript
    // /Users/sunzitong/bash_profile_self/alias.sh 这是我本机shell文件的位置

    alias sonarQube='/Users/sunzitong/Documents/sonarqube-6.7.6/bin/macosx-universal-64/sonar.sh'

    // sonar.sh的路径指向你自己本地的位置
    ```
- **编辑～/.bash_profile文件**

    ```javascript
        // 在底部添加下面的命令，soucre地址为你自己的alias.sh的地址， 如果没有此文件新建一个即可

        source ~/bash_profile_self/alias.sh
    ```

- **运行指令**

    ```javascript
        sunzitong@localhost ~ $ sonarQube start
        Starting SonarQube...
        Started SonarQube

        //打开本地
    ```
### 3、下载vscode插件并进行文件配置

- **下载 SonarQube support for Visual Studio Code**

- **打开 http://localhost:9000/**

    - 初始化的用户名密码均为admin

    - 根据引导进行]生成token（生成之后请保存起来，之后配置要用，token只可以显示一次）

    - 新建一个项目（项目key之后配置要用）

- **在vscode中使用 command + p打开命令搜索功能，输入 >sonar,选择 Create global config with credentials to servers**

    - 打开global.json文件

    - 对servers数组中其中一个对象进行修改

    ```javascript
    // 全局配置文件

        {
            "$schema": "https://raw.githubusercontent.com/silverbulleters/sonarqube-inject-vsc/master/schemas/global.json",
            "servers": [
                {
                    "id": "sunzitong", //与具体工程关联的唯一标识符，在具体工程配置文件中会用到
                    "url": "http://localhost:9000", // sonar server 所在的地址
                    "token": "e7bba68127993ffd7562fcaaa37457d9c42cf8f9" // 之前生成的token
                },
                {
                    "id": "my-company-server",
                    "url": "http://my-company.com",
                    "token": "YOUR_SONARQUBE_AUTH_TOKEN"
                }
            ]
        }
    ```

- **在vscode中使用 command + p打开命令搜索功能，输入 >sonar,选择 Create local sonarlinet config with project binding**

    - 打开sonarlint.json并修改

    ```javascript
    // 工程配置文件
    {
        "$schema": "https://raw.githubusercontent.com/silverbulleters/sonarqube-inject-vsc/master/schemas/sonarlint.json",
        "serverId": "sunzitong", // 即配置全局文件时的 id
        "projectKey": "admin-oms-key" // sonar server 上的工程唯一标识（之前生成的 projectKey）
    }
    ```



### 4、使用

-  在vscode中使用 command + p打开命令搜索功能，输入 >sonar

    - Analyze current file (解析当前文件)

    - Analyze current project (解析当前工程下的所有文件)

    - Update bindings to SonarQube server (更新与服务器相关的数据)
