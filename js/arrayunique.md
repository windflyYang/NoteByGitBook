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
function find(){
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

夏普比率：黄金指标 越高越好 （投资组合预期报酬率-无风险收益）/投资组合的标准差
晨星网 可以去搜索查看夏普比率
买卖基金参考内参数据
