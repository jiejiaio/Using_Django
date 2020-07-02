Django知识点集锦
---
* 系列简介  
    大家好, 在本系列视频中, 我将以短视频的方式逐个讲解Django知识点, 讲解过程中通常会辅以示例代码或截图. 
    
    相比之阅读帮助文档, 也许有些朋友更喜欢视频教程, 这就是本系列视频的目的: 做一个视频版的帮助文档.
    
    我无法保证会一直更新下去. 但我会尽力去做. 
    
    知识点目录参考了官方文档 [**Using Django**](https://docs.djangoproject.com/en/3.0/topics/), 不完全一致.
    
    点击以下的每个章节链接都会跳转到对应的**Branch**, 也可以在Github Branch中搜索你想看的章节
    
    欢迎在 [**Issues**](https://github.com/208352363/Using_Django/issues) 面板中提出你的问题，建议和观点.
* 操作指南 
```shell script
# 克隆仓库到本地
git clone https://github.com/208352363/Using_Django.git
# 查看所有分支(章节), 建议在Git Bash窗口中运行以避免乱码
git branch
# 切换分支(章节) `git checkout 分支名称` 例如:
git checkout Model和数据库-Model-Model简介
```
<details>
  <summary><mark>准备工作</mark></summary>
  <ul>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E5%AE%89%E8%A3%85Python" target="_blank">安装Python</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E5%AE%89%E8%A3%85Git" target="_blank">安装Git</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E5%AE%89%E8%A3%85Pycharm" target="_blank">安装Pycharm</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-(%E5%8F%AF%E9%80%89)%E5%AE%89%E8%A3%85MySQL" target="_blank">(可选)安装MySQL</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-(%E5%8F%AF%E9%80%89)%E5%AE%89%E8%A3%85Postman" target="_blank">(可选)安装Postman</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-(%E5%8F%AF%E9%80%89)%E5%AE%89%E8%A3%85FireFox-Developer-Edition" target="_blank">(可选)安装FireFox Developer Edition</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E5%88%9B%E5%BB%BA%E9%A1%B9%E7%9B%AE(%E4%BD%BF%E7%94%A8Pycharm%E6%88%96%E5%91%BD%E4%BB%A4%E8%A1%8C)" target="_blank">创建项目(使用Pycharm或命令行)</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E5%88%9B%E5%BB%BA%E9%A1%B9%E7%9B%AE(%E4%BD%BF%E7%94%A8Pycharm%E6%88%96%E5%91%BD%E4%BB%A4%E8%A1%8C)#-3" target="_blank">项目的Git和Github配置</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E5%B8%B8%E7%94%A8%E9%85%8D%E7%BD%AE(settings.py)" target="_blank">常用配置(settings.py)</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C-%E6%87%92%E4%BA%BA%E8%BF%90%E8%A1%8Cmanage.py%E7%9A%84%E6%96%B9%E6%B3%95" target="_blank">懒人运行manage.py的方法</a></li>
  </ul>
</details>
<details>
  <summary><mark>Model和数据库</mark></summary>
  <blockquote>
    <details>
      <summary><mark>Model</mark></summary>
      <ul>
        <li><a href="https://github.com/208352363/Using_Django/tree/Model%E5%92%8C%E6%95%B0%E6%8D%AE%E5%BA%93-Model-Model%E7%AE%80%E4%BB%8B" target="_blank">Model简介</a></li>
        <li><a href="https://github.com/208352363/Using_Django/tree/Model%E5%92%8C%E6%95%B0%E6%8D%AE%E5%BA%93-Model-Field%E7%AE%80%E4%BB%8B" target="_blank">Field简介</a></li>
        <li>Field一对一,多对一,多对多</li>
        <li>Model之Meta,属性,方法</li>
        <li>Model继承
          <ul>
            <li>抽象父类</li>
            <li>多表继承</li>
            <li>代理Model</li>
          </ul>
        </li>
      </ul>
    </details>
  </blockquote>
</details>
<details>
  <summary><mark>处理Http请求</mark></summary>
  <blockquote>
    <details>
      <summary><mark>处理URL</mark></summary>
      <ul>
        <li><a href="https://github.com/208352363/Using_Django/tree/%E5%A4%84%E7%90%86Http%E8%AF%B7%E6%B1%82-%E5%A4%84%E7%90%86URL-Django%E5%A6%82%E4%BD%95%E5%A4%84%E7%90%86%E8%AF%B7%E6%B1%82" target="_blank">Django如何处理请求</a></li>
      </ul>
    </details>
  </blockquote>
</details>
<details>
  <summary><mark>使用表单</mark></summary>
  <ul>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E4%BD%BF%E7%94%A8%E8%A1%A8%E5%8D%95-Django%E8%A1%A8%E5%8D%95%E7%AE%80%E4%BB%8B" target="_blank">Django表单简介</a></li>
  </ul>
</details>
<details>
  <summary><mark>处理文件</mark></summary>
  <ul>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E5%A4%84%E7%90%86%E6%96%87%E4%BB%B6-%E5%9C%A8Model%E4%B8%AD%E4%BD%BF%E7%94%A8%E6%96%87%E4%BB%B6" target="_blank">在Model中使用文件</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E5%A4%84%E7%90%86%E6%96%87%E4%BB%B6-%E6%96%87%E4%BB%B6%E5%AF%B9%E8%B1%A1" target="_blank">File对象</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E5%A4%84%E7%90%86%E6%96%87%E4%BB%B6-%E6%96%87%E4%BB%B6%E5%AD%98%E5%82%A8(%E6%96%B9%E5%BC%8F)" target="_blank">文件存储(方式)</a></li>
  </ul>
</details>
<details>
  <summary><mark>用户,认证,授权</mark></summary>
  <ul>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E7%94%A8%E6%88%B7%2C%E8%AE%A4%E8%AF%81%2C%E6%8E%88%E6%9D%83-%E7%AE%80%E4%BB%8B" target="_blank">Django Auth 简介</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E7%94%A8%E6%88%B7%2C%E8%AE%A4%E8%AF%81%2C%E6%8E%88%E6%9D%83-User%E5%AF%B9%E8%B1%A1" target="_blank">User对象</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E7%94%A8%E6%88%B7%2C%E8%AE%A4%E8%AF%81%2C%E6%8E%88%E6%9D%83-%E6%9D%83%E9%99%90%E5%92%8C%E6%9D%83%E9%99%90%E7%BB%84" target="_blank">权限和权限组</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E7%94%A8%E6%88%B7%2C%E8%AE%A4%E8%AF%81%2C%E6%8E%88%E6%9D%83-%E4%BD%BF%E7%94%A8admin%E5%90%8E%E5%8F%B0%E7%AE%A1%E7%90%86%E7%94%A8%E6%88%B7" target="_blank">使用admin后台管理用户</a></li>
    <li><a href="https://github.com/208352363/Using_Django/tree/%E7%94%A8%E6%88%B7%2C%E8%AE%A4%E8%AF%81%2C%E6%8E%88%E6%9D%83-如何实现登录" target="_blank">如何实现登录</a></li>
  </ul>
</details>
