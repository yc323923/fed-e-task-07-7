#### Gridsome基础-介绍

* Gridsome是什么
  - 一个免费、开源、基于Vue.js技术栈的静态网站生成器
  - 官方网站：https://gridsome.org/
  - github：https://github.com/gridsome/gridsome
* 什么是静态网站生成器
  - 静态网站生成器是使用一系列配置、模板以及数据，生成静态HTML文件及相关资源的工具
  - 这个功能也叫预渲染
  - 生成的网站不需要类似PHP这样的服务器
  - 只需要放到支持静态资源的Web Server或CDN上即可运行
* 静态网站的好处
  - 省钱：不需要专业的服务器，只需要托管静态文件的空间即可
  - 快速：不经过后台服务器的处理，只传输静态内容
  - 安全：没有后端程序的执行，自然会更安全
* 常见的静态网站生成器
  - Jekyll(Ruby)
  - Hexo(Node)
  - Hugo(Golang)
  - Gatsby(Node/React)
  - Gridsome(Node/vue)
  - 另外Next.js(React生态)，Nuxt.js(vue生态)也能生成静态网站，但是它们更多被认为是SSR(服务端渲染)框架。
* JAMStack
  - 这类静态网站生成器还有个漂亮的名字叫JAMStack
  - JAMStack的JAM是JavaScript、API和Markup标记语言的首字母组合(也就是说通过JavaScript结合API数据以及Markup标记语言来实现静态网站)，Stack就是技术栈。
  - 本质上是一种胖前端，通过调用各种API来实现更多客户端的功能
  - 其实也是一种前后端的模式，只不过分离得比较开，是一个完全的纯客户端应用，甚至后端可以来自多个不同的厂商。
  - 例如Gridsome，在网站的生成阶段，调用无头CMS，或者是本地文件数据，或者是其他第三方的API接口数据作为静态网站的内容，从WordPress，Contentful或任何其他无头CMS或API中提取数据，并在组件和页面中使用GraphQL访问它。
* 静态应用的使用场景：
  - 不适合有大量路由页面的应用
  - 不适合有大量动态内容的应用




##### Gridsome基础-创建Gridsome项目

* 创建Gridsome项目

* 参考官方文档https://gridsome.org/docs/--->How to install如何创建和启动一个Gridsome项目
  - 安装Gridsome的cli工具
    - Using YARN:yarn global add @gridsome/cli
    - Using NPM:npm install --global @gridsome/cli
* 创建项目
  1. gridsome create my-gridsome-site to create a new project
    - 直接这样创建会很难成功，因为创建gridsome项目依赖了一个特殊的第三方模块sharp(https://github.com/lovell/sharp)，他是用来处理图片的(压缩，转换格式)，这个包很难安装成功：一是以为这个包包含一些C+ +文件，安装时需要对其进行编译才能正常安装，得有一个C++环境才可以，二是因为sharp还依赖了一个libvips的模块,libvips有几十兆，由于国内的网络环境也很难下载成功，最终导致sharp很难安装成功
    - 解决以上两个问题就是设置镜像
        - 打开sharp的官网https://sharp.pixelplumbing.com/
        - 在Installation中可以看到安装的指引，找到Chinese mirror部分提供了中国镜像(淘宝镜像)，这里提供了2中配置方式：一是npm，一是配置环境变量，都可以，这里采用npm
          ```bash
          npm config set sharp_binary_host "https://npm.taobao.org/mirrors/sharp"
          npm config set sharp_libvips_binary_host "https://npm.taobao.org/mirrors/sharp-libvips"
          // npm install sharp 这里不用安装，因为在创建Gridsome项目时会自动安装
          ```
       - C++编译的问题，也就是得有个C+ +环境：
          - 这里安装node-gyp(https://github.com/nodejs/node-gyp)以及他的编译套件，他的作用就是编译nodejs中C+ +扩展包的
            ```bash
            npm install -g node-gyp
            ```
          - 安装好之后还不能直接使用，因为还需安装依赖也就是编译套件
          - 注意：本地必须已经安装了Pathon
          ```bash
          // 注意：需要以管理员身份运行安装
          npm install --global windows-build-tools
          // 如果总失败，可安装指定版本 
          npm install --global --production windows-build-tools@4.0.0
          ```
  2. cd my-gridsome-site to open folder
    ```bash
    npm run develop
    ```
  3. gridsome develop to start local dev server at http://localhost:8080