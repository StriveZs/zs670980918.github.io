---
title: Hexo中归档页美化

categories:
  - 文章页
  - Hexo
  - Next主题

tags:
  - 美化
  - hexo
  - next
  - archive
---

# Hexo中归档页美化
## 配置
### 配置代码
1. 修改 /themes/next/layout/_macro/post-collapse.swig 后的代码如下：
```
{% macro render(post) %}

  <article class="my-post post-type-{{ post.type | default('normal') }}" itemscope itemtype="http://schema.org/Article">
    <header class="my-post-header">

      <div class="my-post-meta">
        <time class="my-post-time" itemprop="dateCreated"
              datetime="{{ moment(post.date).format() }}"
              content="{{ date(post.date, config.date_format) }}" >
          {{ date(post.date, 'MM-DD') }}
        </time>
      </div>

      <{% if theme.seo %}h3{% else %}h2{% endif %} class="my-post-title">
        {% if post.link %}{# Link posts #}
          <a class="my-post-title-link post-title-link-external" target="_blank" href="{{ url_for(post.link) }}" itemprop="url">
            {{ post.title or post.link }}
            <i class="fa fa-external-link"></i>
          </a>
        {% else %}
            <a class="my-post-title-link" href="{{ url_for(post.path) }}" itemprop="url">
              {% if post.type === 'picture' %}
                {{ post.content }}
              {% else %}
                <span itemprop="name">{{ post.title | default(__('post.untitled')) }}</span>
              {% endif %}
            </a>
        {% endif %}
      </{% if theme.seo %}h3{% else %}h2{% endif %}>

    </header>
  </article>

{% endmacro %}
```
2. 在 /themes/next/source/css/_custom/custom.styl 新增如下样式:
```
/* 归档页样式 began */
.page-archive .archive-page-counter {
  font-size: 18px;
  background-color: #49b1f5;
  padding-left: 10px;
  padding-right: 10px;
  border-radius: 8px;
  color: #fff;
  +mobile() {
    font-size: 16px;
  }
}
.my-post-time{
  font-size: 11px;
  position: absolute;
  color: #fff;
  background-color: #49b1f5;
  border-radius: 5px;
  padding-left: 5px;
  padding-right: 5px;
  margin-left: 15px;
}
.mypost{
  position: relative;
  margin-bottom: 1rem;
  -webkit-transition: all .2s ease-in-out;
  -moz-transition: all .2s ease-in-out;
  -o-transition: all .2s ease-in-out;
  -ms-transition: all .2s ease-in-out;
  transition: all .2s ease-in-out;
}
a.my-post-title-link:before{
  top: 10px;
  width: 18px;
  height: 18px;
  content: "📚";
  margin-right: 5px;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: 15px;
  line-height: 18px;
}
.my-post:hover{
  transform: scale(1.1);
  box-shadow: 10px 10px 15px 2px rgba(0,0,0,.12), 0 0 6px 0 rgba(104, 104, 105, 0.1);
  border-radius: 30px;
  width: 400px;
  padding: 1px 10px;
  margin-left: 25px;
  font-size: 16px;
  transition-duration: 0.15s;
  +mobile(){
    width: 260px;
    margin-left: 18px;
  }
  //display:flex;
}
a.my-post-title-link{
  text-decoration: none;
  font-size: 15px;
  font-weight: 400;
  +mobile() {
    font-size: 14px;
  }
}
.my-post-title{
  display: block;
  margin-left: 4.5rem;
  color: #4c4948;
  text-decoration: none;
  font-size: .8rem;
  cursor: pointer;
  +mobile() {
    //margin-left: 4rem;
  }
}
.my-post-header{
  position: top;
  margin-bottom: 1rem;
  -webkit-transition: all .2s ease-in-out;
  -moz-transition: all .2s ease-in-out;
  -o-transition: all .2s ease-in-out;
  -ms-transition: all .2s ease-in-out;
  transition: all .2s ease-in-out;
}
//.my-post-title-link{
//  font-size: 16px;
//  font-weight: 500;
//}
.my-post-meta{
  position: absolute;
  color: #99a9bf;
  width: 80px;
  color: #114142;
}
div.post-block.tag .collection-title h2 {
  border-width: 1px;
  border-style: solid;
  border-color: #3f3f3f;
  border-radius: 20px;
  font-size: 22px;
  background-color: #b4e8fa;
  padding: 2px 15px;
  letter-spacing: 1.5px;
  box-sizing: border-box;
  color: #3f3f3f;
  display: inline-block;
  margin: 10px 0 10px;
  text-align: center;
  +mobile(){
    font-size: 18px;
  }
}
.category-list-link:hover{
  transform: scale(1.1);
  box-shadow: 10px 10px 15px 2px rgba(0,0,0,.12), 0 0 6px 0 rgba(104, 104, 105, 0.1);
  border-radius: 8px;
  padding: 1px 1px;
  margin-left: 5px;
  font-size: 16px;
  transition-duration: 0.15s;
  //display:flex;
}
/* 归档页样式 end */
```

## 效果图
![figure](https://gitee.com/zyp521/upload_image/raw/master/svg2B6.png)