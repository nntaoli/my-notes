### git fatal: 拒绝合并无关的历史的错误解决  

> 本地初始化的项目 与 github 版本不一致, 导致无法提交     

解决方法, 在pull 时候, 添加`–allow-unrelated-histories`参数 即可.  

> git pull origin master --allow-unrelated-histories   


