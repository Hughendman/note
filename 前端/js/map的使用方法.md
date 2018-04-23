```
var data = [1, 2, 3, 4];

var arrayOfSquares = data.map(function (item) {
    return item * item;
});
console.log(arrayOfSquares);

```
```
var content = header.map(function(item,index,arr){//数据信息
			if(!col.includes(item.name) && !row.includes(item.name)){
				return item;
			}
		},[]).filter(function(item){
			console.log(item);
			if(item != undefined){
				return item;
			}
		});
		
```