> 埋点上传主要分为三种
无埋点（收集所有数据后端处理），可视化埋点以及代码埋点



```

(function() {
	function JW() {
		this.siteId = "1234";
		this.rpDomain = "http://js.test.com:8000/s.gif";
		this.uuid = "uuid-1";
		this.env = {};
		this.init();
	}
	var d = document,
	w = window,
	f = encodeURIComponent;
	function g(a, b) {
		try {
			var c = [];
			c.push("name=" + f(a.name));
			c.push("msg=" + f(a.message));
			c.push("page=" + f(w.location.href));
			c.push("ex=" + f(b));
			c.push("rnd=" + Math.floor(2147483648 * Math.random())); (new Image).src = "http://js.test.com:8000/err.gif?" + c.join("&")
		} catch(d) {
			console.log(d)
		}
	}

	JW.prototype = {
		init: function() {
			try {
				this.getLan();
				this.getScreen();
				this.getTitle();
				this.setHandler();
			} catch(a) {
				g(a, "i")
			}
		},
		getLan: function() {
			try {
				this.env.lan = w.navigator.systemLanguage || w.navigator.language;
				this.env.lan = this.env.lan.toLowerCase();
				return this.env.lan;
			} catch(a) {
				g(a, "sl")
			}
		},
		getScreen: function() {
			try {
				return this.env.scr = (w.screen.width && w.screen.height ? w.screen.width + "x" + w.screen.height: "0x0"),
				this.env.scr;
			} catch(a) {
				g(a, "ss")
			}
		},
		getTitle: function() {
			try {
				var a = d.title;
				40 < a.length && (a = a.substr(0, 40), a += "...");
				return this.env.tl = a,
				this.env.tl;
			} catch(b) {
				g(b, "gt")
			}
		},
		setHandler: function() {
			try {
				var a = this;
				w._jwo = {
					push: function() {
						return a.doHandle.apply(a, arguments)
					}
				}
			} catch(b) {
				g(b, "op")
			}
		},
		doHandle: function(a) {
			try {
				if ("[object Array]" === {}.toString.call(a)) switch (a[0]) {
				case "_pv":
					var c = ["_act=_pv"];
					this.report(c);
					break;
				case "_event":
					var c = [];
					a[1] && a[2] && (c.push("_ct=" + a[1]), c.push("_act=" + a[2]), c.push(a[3] ? "_lb=" + f(a[3]) : ""), c.push(a[4] ? "_v=" + f(a[4]) : ""), c.push(a[5] ? a[5] : ""), this.report(c));
					break;
				}
			} catch(u) {
				g(u, "dh")
			}
		},

		report: function(arr) {
			try {
				var data = [];
				data.push("_uid=" + this.uuid);
				for (k in this.env) {
					data.push("_" + k + "=" + f(this.env[k]));
				}
				for (j = 0, len = arr.length; j < len; j++) {
					if (arr[j]) {
						data.push(arr[j]);
					}
				}
				var url = this.rpDomain + "?" + data.join('&');
				this.imgRequest(url);
			} catch(d) {
				g(d, "rd")
			}
		},
		imgRequest: function(url) {
			try {

				var imageName = "_jw_img" + Math.floor(2147483648 * Math.random());
				w[imageName] = new Image();
				w[imageName].a = imageName;
				w[imageName].onload = w[imageName].onerror = w[imageName].onabort = function() {
					try {
						this.onload = this.onerror = this.onabort = null,
						w[this.a] = null
					} catch(l) {}
				};
				w[imageName].src = url + "&_r=" + Math.floor(2147483648 * Math.random())
			} catch(l) {
				g(l, "ir")
			}
		},

	};

	try {
		var j = new JW();
		j.doHandle(["_pv"]);
	} catch(a) {
		g(a, "m")
	}
	//当采取无埋点方式时，采用下面的方法
	document.addEventListener("click",function(e){
      console.log(document.cookie);
      console.log(e.target.innerText);
    })

})();
```