# Uni-app_program_shop

#### 00 readme：

- 本项目数据接口运行在本地服务器，需安装本地接口服务器。

#### 01 安装本地接口服务器：

- 安装phpStudy 并且启动；
- 点击 MySQL管理器 - MySQL-Front
- 新建数据库，名称：dtcmsdb4
- 右键dtcmsdb4数据库 - 输入 - SQL文件，选择dtcmsdb4.sql，修改字符集：UTF-8
- 在dtcmsdb4.sql文件目录下运行powershell或终端（shift+右键），输入npm i 
- 运行数据库服务：node ./src/app.js
- 本地接口地址：http://localhost:8082/ + “接口地址”

#### 02 本地数据接口：

##### 2.1 轮播图接口

- 接口地址：/api/getlunbo
- 请求方式：GET
- 参数：无

##### 2.2 商品列表

- 接口地址：/api/getgoods?pageindex=number
- 请求方式：GET
- 参数：pageindex: 页码；传递方式：/api/getgoods?pageindex=1

##### 2.3 详情轮播图

- 接口地址： /api/getthumimages/:imgid
- 请求方式：GET
- 参数： imgid: 图片id，传入url写法：/api/getthumimages/43

##### 2.4 详情参数

- 接口地址：  /api/goods/getinfo/:id
- 请求方式：GET
- 参数：Id:商品主键值 /api/goods/getinfo/100

##### 2.5 详细介绍

- 接口地址：  /api/goods/getdesc/:id
- 请求方式：GET
- 参数：Id：商品数据的id  Url ： /api/goods/getdesc/87

##### 2.6 图片分类

- 接口地址： /api/getimgcategory
- 请求方式：GET
- 参数：无

##### 2.7 二级图片列表

- 接口地址：/api/getimages/:cateid
- 请求方式：GET
- 参数：cateid: 图片的类别id，传入url写法： /api/getimages/23

##### 2.8 资讯列表

- 接口地址：/api/getnewslist
- 请求方式：GET
- 参数：无

##### 2.9 资讯详情

- 接口地址：/api/getnew/:newid
- 请求方式：GET
- 参数：newid:资讯id，传入url写法： /api/getnew/43





