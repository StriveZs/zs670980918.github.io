---
titile: PHP+XML+DTD+HTML 编写的在线词典

categories:
  - PHP
  - XML

tags:
  - PHP
  - XML
  - DTD
  - 词典

mathjax: true

---

# PHP+XML+DTD+HTML 编写的在线词典
## view
### 主界面
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>操作页面</title>
</head>
<body>
    <h1>查询单词</h1>
    <form action="/study/XML学习/词典系统/control/search.php" method="post">
        输入你要查询的英文的单词: <input type="text" name="english">
        <br/>
        <input type="submit" value="查询">
    </form>
    <h1>添加单词</h1>
    <form action="/XML学习/词典系统/control/addDict.php" method="post">
        英文: <input type="text" name="eng">
        中文: <input type="text" name="chi">
        <input type="submit" value="提交">
    </form>
</body>
</html>
```

### 查询成功界面
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>查询结果页面</title>
</head>
<body>
<h1>查询结果为<?php echo $_GET['chinese']; ?></h1>
</body>
</html>
```

### 查询失败界面
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>查询结果失败页面</title>
</head>
<body>
<h1>没有该单词!</h1>
</body>
</html>
```

## control
### 查询单词
```
<?php
    function getNodeValue(&$myNode,$tagName){
        return $myNode->getElementsByTagName($tagName)->item(0)->nodeValue;
    }

    $word = $_POST['english'];

    // 创建DOCDocument对象
    $xmlDoc = new DOMDocument();
    // 加载xml文件
    $xmlDoc->load("/XML学习/词典系统/model/dict.xml");
    // 查询单词
    $wordList = $xmlDoc->getElementsByTagName("单词");
    $index = -1;
    for($i=0;$i<$wordList->length;$i++){
        $result = getNodeValue($wordList[$i],"英文");
        if($result == $word){
            $index = $i;
            break;
        }
    }
    if($index == -1){
        header("Location:/XML学习/词典系统/view/failed.html");
    }
    else{
        $chinese= getNodeValue($wordList[$index],"中文");
        $encode = urlencode($chinese);
        header("Location:/XML学习/词典系统/view/mess.php?chinese=$encode");
    }

?>
```

### 添加单词
```
<?php
    function getNodeValue(&$myNode,$tagName){
        return $myNode->getElementsByTagName($tagName)->item(0)->nodeValue;
    }
    $eng = $_POST['eng'];
    $chi = $_POST['chi'];

    // 先判断单词是否存在，如果存在则不添加，并提示
    // 创建DOCDocument对象
    $xmlDoc = new DOMDocument();
    // 加载xml文件
    $xmlDoc->load("/XML学习/词典系统/model/dict.xml");
    // 查询单词
    $wordList = $xmlDoc->getElementsByTagName("单词");
    $index = -1;
    for($i=0;$i<$wordList->length;$i++){
        $result = getNodeValue($wordList[$i],"英文");
        if($result == $eng){
            $index = $i;
            break;
        }
    }
    if($index != -1){
        echo "<script>window.alert('单词已经存在! 添加失败');history.back();</script>";
    }
    else{
        // 得到根节点n
        $root = $xmlDoc->getElementsByTagName("词典")->item(0);
        // 创建单词节点
        $new_word = $xmlDoc->createElement("单词");
        // 创建中文节点
        $new_chi = $xmlDoc->createElement("中文");
        $new_chi->nodeValue = $chi;
        // 创建英文节点
        $new_eng = $xmlDoc->createElement("英文");
        $new_eng->nodeValue = $eng;

        // 将节点挂载
        $new_word->appendChild($new_eng);
        $new_word->appendChild($new_chi);
        $root->appendChild($new_word);

        // 保存xml文件
        $xmlDoc->save("/个人文件/study/XML学习/词典系统/model/dict.xml");
        echo "<script>window.alert('单词保存成功!');history.back();</script>";
    }
?>
```

## model
### 存储单词文件
xml文件
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE 词典 SYSTEM "dict.dtd">
<!--引入dtd文件-->
<!--班级 根元素-->
<词典>
    <单词>
        <英文>boy</英文>
        <中文>男孩</中文>
    </单词>
<单词><英文>girls</英文><中文>女孩</中文></单词></词典>

```

### DTD文件
```
<!ELEMENT 词典 (单词+)>
    <!ELEMENT 单词 (英文,中文)>
        <!ELEMENT 英文 (#PCDATA)>
        <!ELEMENT 中文 (#PCDATA)>
```

## 展示
![figure.1](https://gitee.com/zyp521/upload_image/raw/master/NkX3bj.png)

![figure.2](https://gitee.com/zyp521/upload_image/raw/master/ilIfqN.png)

![figure.3](https://gitee.com/zyp521/upload_image/raw/master/hjVnNG.png)

![figure.4](https://gitee.com/zyp521/upload_image/raw/master/wKh5qo.png)

![figure.5](https://gitee.com/zyp521/upload_image/raw/master/JI4NdI.png)