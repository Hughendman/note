```
 $document.on(
"click",
function(e){
    let dom = e.target.getAttribute("data");
    $scope.$apply(function (e) {
        if(dom && dom == "checkOpen"){
            $scope.showCheck = $scope.showCheck ? false : true;
        }else if(!dom || dom != "check"){
            $scope.showCheck = false;
        }
    });
});

```

使用$apply可以实时刷新dom。