## title
>   Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

> 给定一个n个整数的数组，a、b、c在S中是a + b + c = 0 ?在数组中找到所有的唯一的三联，它们的和为零。

## code

> es6

```
var threeSum = function(nums) {
    let sum, right, left
    const result = []
    nums.sort((a, b) => a - b).forEach((n, i) => {
        [left, right] = [i+1, nums.length-1]
        if (n !== nums[i-1]) while (left < right) {
            sum = n + nums[left] + nums[right]
            if (sum === 0) {
                result.push([n, nums[left], nums[right]])
                while (left < right && nums[left] === nums[left+1]) ++left
                while (left < right && nums[right] === nums[right-1]) --right
                --right;++left
            }
            else if (sum > 0) --right
            else ++left
        }
    })

    return result
};

```

> es5

```
//思路： 两层循环搞定，首先需要排序，第一层循环是的最后一位+当前位+当前位的后一位，为0则ok，否则的话判断和的大小来数进行移位，大于0 ，right向前移，小于0，letf向后移
var threeSum = function threeSum(nums) {
        var sum = void 0,
            right = void 0,
            left = void 0;
        var result = [];
        nums.sort(function (a, b) {  //排序
            return a - b;
        }).forEach(function (n, i) { //循环
            left = i + 1;  // 后一位的索引
            right = nums.length - 1; // 最后一位的索引
            if (n !== nums[i - 1]) while (left < right) { // 排重 + 循环
                sum = n + nums[left] + nums[right];
                if (sum === 0) {
                    result.push([n, nums[left], nums[right]]);
                    while (left < right && nums[left] === nums[left + 1]) {
                        ++left;
                    }while (left < right && nums[right] === nums[right - 1]) {
                        --right;
                    }--right;++left;
                } else if (sum > 0) --right;else ++left;
            }
        });

        return result;
    };
    threeSum([-4,-5,1,2,3,4,5,6,7,8,9]);

```

## readme

> console.log(threeSem([1,0,-1,2,-2]));

> [Array(3), Array(3)]
0:(3) [-2, 0, 2]
1:(3) [-1, 0, 1]