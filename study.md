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


3. switch条件
// 冗余
switch (data) {
  case 1:
    test1();
  break;

  case 2:
    test2();
  break;

  case 3:
    test();
  break;
  // so on...
}

// 简洁
var data = {
  1: test1,
  2: test2,
  3: test
};

data[anything] && data[anything]();

4.重复字符串多次
// 冗余
let test = ''; 
for(let i = 0; i < 5; i ++) { 
  test += 'test '; 
} 

// 简洁
'test '.repeat(5);


