**数组去重**
```
let test = [1,3,9,1,4,3,5,6]
[...newSet(test)];

Array.from(new Set(test))

function unique(arr) {
    const res = new Map();
    return arr.filter((a) => !res.has(a) && res.set(a, 1))
}

var arr = [1,3,4,5,6,7,4,3,2,4,5,6,7,3,2];
function find(arr){
    var newArr = [];
    for (var i = 0; i < arr.length; i++) {
      if (newArr.indexOf(arr[i]) == -1 ) {
        newArr.push(arr[i]);
      }
    }
    return newArr;
 }
find(arr);
```

排序数组的去重
基本思路
数组完成排序后，我们可以放置两个指针 i 和 j，其中 i 是慢指针，而 j 是快指针。只要 nums[i] === nums[j]，我们就增加 j 跳过重复项。
当我们遇到 nums[j] !== nums[i] 时，跳过重复项的运行已经结束，因此我们必须把nums[j]的值复制到 nums[i + 1]。
然后递增 i，接着我们将再次重复相同的过程，直到 j 到达数组的末尾为止。
var removeDuplicates = function(nums) {
  // 特判
  if (nums.length === 0) {
    return 0
  }
  let i = 0
  for (j = 1; j < nums.length; j++) {
    if (nums[j] !== nums[i]) {
      i++
      nums[i] = nums[j]
    }
  }
  return i + 1
};

作者：文斌大大鸟
链接：https://juejin.cn/post/6930816978101747725
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

夏普比率：黄金指标 越高越好 （投资组合预期报酬率-无风险收益）/投资组合的标准差
晨星网 可以去搜索查看夏普比率
买卖基金参考内参数据
