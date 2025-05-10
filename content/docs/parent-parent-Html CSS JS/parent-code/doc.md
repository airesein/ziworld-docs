+++
title = "doc.html"
icon = "article"
toc = true
+++
``` html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>

</head>

<body>
    <div id="block"></div>
    <div class="cont">
        <p>默认的文本</p>
        <p class='itm'>默认的文本</p>
        <p class="itm">默认的文本</p>
        <p>默认的文本</p>
    </div>
    <script>
        var block= document.getElementById('block')
        console.log(block)
        block.textContent = '重置的文本'

        var p=document.querySelectorAll('.cont p')
        //p = document.getElementsByTagName('p')
        console.log(p)
        newArr = ['我还是', '从前那个', '少年','没有']
        for (var i = 0; i <= p.length; i++) {
            p[i].textContent = newArr[i]
        }

        var secItm=document.querySelector('.itm')
        secItm.textContent='替换后的'
    </script>
</body>

</html>
```