Django知识点集锦
---
* 系列简介  
    大家好, 在本系列视频中, 我将以短视频的方式逐个讲解Django知识点, 讲解过程中通常会辅以示例代码或截图. 
    
    相比之阅读帮助文档, 也许有些朋友更喜欢视频教程, 这就是本系列视频的目的: 做一个视频版的帮助文档.
    
    我无法保证会一直更新下去. 但我会尽力去做. 
    
    知识点目录参考了官方文档 [**Using Django**](https://docs.djangoproject.com/en/3.0/topics/), 不完全一致.
    
    点击以下的每个章节链接都会跳转到对应的**Branch**, 也可以在Github Branch中搜索你想看的章节
    
    欢迎在 [**Issues**](https://github.com/208352363/Using_Django/issues) 面板中提出你的问题，建议和观点.
* 准备工作
    * [安装Python](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E5%AE%89%E8%A3%85Python)
    * [安装Git](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E5%AE%89%E8%A3%85Git)
    * [安装Pycharm](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E5%AE%89%E8%A3%85Pycharm)
    * [(可选)安装MySQL](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-(%E5%8F%AF%E9%80%89)%E5%AE%89%E8%A3%85MySQL)
    * [(可选)安装Postman](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-(%E5%8F%AF%E9%80%89)%E5%AE%89%E8%A3%85Postman)
    * [(可选)安装FireFox Developer Edition](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-(%E5%8F%AF%E9%80%89)%E5%AE%89%E8%A3%85FireFox-Developer-Edition)
    * [创建项目(使用Pycharm或命令行)](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E5%88%9B%E5%BB%BA%E9%A1%B9%E7%9B%AE(%E4%BD%BF%E7%94%A8Pycharm%E6%88%96%E5%91%BD%E4%BB%A4%E8%A1%8C))
    * [项目的Git和Github配置](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E5%88%9B%E5%BB%BA%E9%A1%B9%E7%9B%AE(%E4%BD%BF%E7%94%A8Pycharm%E6%88%96%E5%91%BD%E4%BB%A4%E8%A1%8C))
    * [常用配置(settings.py)](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E5%B8%B8%E7%94%A8%E9%85%8D%E7%BD%AE(settings.py))
    * [懒人运行manage.py的方法](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E6%87%92%E4%BA%BA%E8%BF%90%E8%A1%8Cmanage.py%E7%9A%84%E6%96%B9%E6%B3%95)
* Model和数据库
    * Model
        * [Model简介](https://github.com/208352363/Using_Django/tree/Model%E5%92%8C%E6%95%B0%E6%8D%AE%E5%BA%93-Model-Model%E7%AE%80%E4%BB%8B)
        * [Field简介](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%)
        * [Field一对一,多对一,多对多](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%)
        * [Model之Meta,属性,方法](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%)
        * Model继承
            * [抽象父类](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%)
            * [多表继承](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%)
            * [代理Model](https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%)