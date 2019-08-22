### 基本说明
* uaas用于系统用户，normal-account用于普通用户
* 系统用户和普通用户具有相同的注册、登陆流程
* 系统用户、普通用户登录后得到的token加密key不一样，拥有的能力也不一样
* 系统用户拥有资源、角色和权限，可以访问系统受限api
* 普通用户视为部门一种资源，不具备角色和权限，只能访问特定api(/api/u/**)，这些特定api系统用户不能访问
* 注册方式有两种，通过手机号码（未实现），通过邮箱

### 注册流程，以邮箱为例
* 用户填写邮箱、账号密码
* 获取验证码，注册（[接口调用](https://github.com/zelejs/saas-test-cases/blob/master/uaas/邮箱验证码及注册.md)）

### 登陆
根据swagger提示，使用登陆rest api

### Swagger
* 系统用户注册登陆（[查看](http://192.168.3.28:8088/swagger-ui.html#/sys-user-endpoint)）
* 系统用户信息（[查看](http://192.168.3.28:8088/swagger-ui.html#/profile-endpoint)）
* 系统用户crud（[查看](http://192.168.3.28:8088/swagger-ui.html#/admin-user-endpoint)）
* 普通用户注册登录（[查看](http://192.168.3.28:8088/swagger-ui.html#/normal-account-pub-endpoint)）
* 普通用户crud（[查看](http://192.168.3.28:8088/swagger-ui.html#/normal-account-endpoint)）
