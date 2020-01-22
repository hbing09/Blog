# Amazon Clone 项目文档

# 概括


# Tools
| Tools          | Usage                        |
| -------------- | ---------------------------- |
| Vue.js         | Frontend                     |
| Node.js        | Backend                      |
| MongoDB        | data storage                 |
| AWS            | image storage and deployment |
| Stripe, Paypal | payment                      |
| Algolia        | search engine                |

# Node.js
## 什么是 Node？

是 javascript 的一中运行环境。我们都知道 JS 都是在浏览器中执行的,用于给网页添加各种动态效果，name 可以说浏览器也是 JS 的运行环境。

## 浏览器 JavaScript 和 Node 的关系和区别
![ECMAScript 是 JavaScript 的规格，后者是前者的一种实现，一般这两个词可以互换](https://paper-attachments.dropbox.com/s_F58BD128A927F436A9A7AEFB7D0482801F853752076CC1EAE2CD9A7A7699357F_1579549657496_image.png)


浏览器端的 JS 还包括：

    - 浏览器对象模型 BOM， window 对象
    - 文档对象模型 DOM，document对象

Node 则包括 V8 引擎，V8 是 chrome 浏览器中的 JS 引擎
Node 将 V8 进一步加工成可在任何操作系统中运行 JS 的平台。
简而言之，Node 为我们提供了一个无需依赖浏览器、能够直接与操作系统进行交互的 JavaScript 代码运行环境！

## Node 全局对象初探
![](https://paper-attachments.dropbox.com/s_F58BD128A927F436A9A7AEFB7D0482801F853752076CC1EAE2CD9A7A7699357F_1579551497222_image.png)


**process**
`process` 全局对象可以说是 Node.js 的灵魂，它是管理当前 Node.js 进程状态的对象，提供了与操作系统的简单接口。
`process` 对象的一些属性：

- `pid`：进程编号
- `env`：系统环境变量
- `argv`：命令行执行此脚本时的输入参数
- `platform`：当前操作系统的平台

**Buffer**
`Buffer` 全局对象让 JavaScript 也能够轻松地处理二进制数据流，结合 Node 的流接口（Stream），能够实现高效的二进制文件处理

`**__filename**` **和** `**__dirname**`
分别代表当前所运行 Node 脚本的文件路径和所在目录路径。

setTimeout 用于设置 等待多长时间后要执行什么函数，但是在等待的这段时间内，程序并没有阻塞，而是继续向下执行，这就是 Node 的异步非阻塞！
在实际的应用环境中，往往有很多 I/O 操作（例如网络请求、数据库查询等等）需要耗费相当多的时间，而 Node.js 能够在等待的同时继续处理新的请求，大大提高了系统的吞吐率。

## Node 的模块机制

JS 语言本身没有模块化的机制，通常使用一系列<script>标签来导入相应的模块，导致了很多问题：

    - 多个 JS 文件直接作用于全局命名空间，命名冲突
    - JS 文件之间不能互相访问
    - 导入的<script>无法被轻易修改

**什么是Node 模块**

    - 核心模块：Node 提供的内置模块
    - 文件模块：用户编写的，可以是.js .node .json文件，也可以是目录 package.json, index

**如何实现？**

- require → **模块标识符,** 用于导入其他 Node 模块
- exports → 写一个 Node 模块，导出其中的内容
- module → 
****## npm scripts 的基本概念和使用

npm scripts 看上去平淡无奇，但是却能为项目开发提供非常便利的工作流。例如，之前构建一个项目需要非常复杂的命令，但是如果你实现了一个 `build` npm 脚本，那么当你的同事拿到这份代码时，只需简单地执行 `npm run build` 就可以开始构建，而无需关心背后的技术细节。

## 特点
- **单线程 →** 每个请求将生产一个线程，这种方法避免了 CPU 上下文切换和内存中的大量执行堆栈
- **非阻塞 I/O →** 避免了由于需要等待输入或者输出响应而造成的 CPU 时间损失，得益于异步 I/O。
- **事件驱动编程 →** 事件与回调确是一种高性能的服务模型
- **跨平台**


## 参考
****
https://interview.nodejs.red/#/

https://zhuanlan.zhihu.com/p/100071394

# Frontend
## consumer facing frontend
    1. 首页
****        - Nav bar | search bar
        - Side bar | Featured products
        - Listing Products
        - Footer
                **Use axios call to map the data to the listing tag**
    2. 产品页
        - Image | description | add to cart
        - About author
        - Reviews
## admin frontend
****    1. to store the products
    2. to create categories
    3. to create owner of the product

DOM: document object model

    index.vue 是 home page，这个 file 会被 automatically render，我们需要加什么 page，直接在 pages 这个 folder 里加上相应的 vue 文件，
# Backend
# Authentication

json web token

![](https://paper-attachments.dropbox.com/s_F58BD128A927F436A9A7AEFB7D0482801F853752076CC1EAE2CD9A7A7699357F_1579501368722_image.png)


browser will store the “json web token” in local or cookie and will be used later, middleware will check whether the token is valid

signup API and login API 
sign up 
就是用两个 library：jsonwebtoke 和 bcrypt-nodejs，用来把原用户名和密码加密存成 json 的格式，浏览器缓存在 local 或者 cookie 里面，之后用的时候，JWT middleware 会request 这个 json 文件，verify 这个 token 是否正确。
log in
要比较输入的密码和存储的密码的 hash 之后的加密格式，看是否一致

logout → login = false

review , average rating and fixing bugs → save virtual,  sum/reviews
address → third party API to get the list of countries

VUEX
a giant javascript object, a statement management, 
like login = false, navbar = false

![](https://paper-attachments.dropbox.com/s_F58BD128A927F436A9A7AEFB7D0482801F853752076CC1EAE2CD9A7A7699357F_1579505779239_image.png)

![](https://paper-attachments.dropbox.com/s_F58BD128A927F436A9A7AEFB7D0482801F853752076CC1EAE2CD9A7A7699357F_1579505806044_image.png)


Stripe
used for payment, 

****
- State management by creating an add to cart feature
- Payment integration
- Search Integration
- Forms
- MongoDB database
- Redis - how to access fast data
- build your own web application by the end of the course
- deploy your application AWS
- AWS S3 to store images
- Authentication

