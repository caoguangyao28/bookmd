```
//数组属性及方法
//push unshift pop shift reverse splice sort
//1, splice 使用示例
// 可以起到删除 添加 替换 的效果
var arr = [1,2,3,4];
arr.splice(2,2);
arr.splice(2,0,3,4);
arr.splice(-1,0,6,7,8);
arr.splice(3,3);
//2, sort 使用示例
//数组排序 sort 默认按照 ascll 排序的
var arr2 = [29,47,5,7];
console.log(arr2.sort());
arr2.sort(function(a,b){//冒泡排序
    return a-b;
});
var objarr = [{name:'1',age:10},{name:'2',age:8},{name:'3',age:20}];
objarr.sort(function(a,b){
    return a.age - b.age;
});
//数据随机排序 random() (0,1);
var arr3 = [1,2,3,4,5,6];
arr3.sort(function(a,b){
   var tem = Math.random();
   return tem-0.5;
});
console.log(arr3);
//按字节排序数组
var arrSortBype = ['你好','hello','ok','程序员'];
//获取字符串的字节数
function getBytes(str){
    var bytes = str.length;
    for(var i=0;i<str.length;i++){
        if(str.charCodeAt(i) > 255){//中文时 占2个字节
            bytes++
        }
    }
    return bytes;
}
arrSortBype.sort(function(a,b){
   return getBytes(a)-getBytes(b);
});
console.log(arrSortBype);
//以上都是在原有数组上进行修改 
//返回新数组
concat  slice  toString  join  (字符串方法 split)
// 类数据 函数内置参数 argument 以及 document.get... 获取返回值
// 模拟类数组


//数组去重
Array.prototype.unique = function () {
    var temp = {},resArr=[];
    for (var i=0;i< this.length;i++){
        if(!temp.hasOwnProperty(this[i])){
            temp[this[i]] = this[i];
            resArr.push(this[i]);
        }
    }
    return resArr;
};

//字符串去重
      
```
![图片](https://uploader.shimo.im/f/v6Jun8nvkjw0l8lk.png!thumbnail)

