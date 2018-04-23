```
$scope.$watch('rooturl',function () {
    if($scope.rooturl==='/analysis/subordinateDataAnalysis'){
        $scope.navsUrl='/analysis/subordinateDataAnalysis';
    }
    if($scope.rooturl==='/analysis/singleStore'){
        $scope.navsUrl='/analysis/singleStore';
    }
});

```