1. if多条件判断
// 冗余
if (x === 'abc' || x === 'def' || x === 'ghi' || x ==='jkl') {}
// 简洁
if (['abc', 'def', 'ghi', 'jkl'].includes(x)) {}

2. 函数条件调用
// 冗余
function test1() {
  console.log('test1');
};
function test2() {
  console.log('test2');
};
var test3 = 1;
if (test3 == 1) {
  test1();
} else {
  test2();
}

// 简单
(test3 === 1? test1:test2)();

3. 

