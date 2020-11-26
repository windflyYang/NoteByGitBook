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