## 代码

```
function track(name,content) {
    function JW(name,content){
        this.url =  "http://js.test.com:8000/s.gif";
        this.content = content;
        this.name = name;
    }
    JW.prototype = {
        init: function () {
            this.getName();
            this.creatGif();
        },
        creatGif: function () {
            var img = new Image();
            img.onload = function(){console.log("img is loaded")};
            img.onerror = function(){console.log("error!")};
            img.src = this.url;
        },
        getName: function () {
            this.url = this.url + "?content=" + this.content + "&name=" + this.name;
        }

    }
    var JW = new JW(name,content);
    JW.init();
};

export{
  track
}

```

## 使用方法

```
import {track} from './../../static/maidian'

track(content,name);

```

