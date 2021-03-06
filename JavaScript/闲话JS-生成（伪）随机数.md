# 生成（伪）随机数

为什么说是伪随机数？因为真正意义上的随机数是通过真实的物理现象（随机事件）产生的，其结果无法预测。而计算机生成的随机数都是通过某种算法来实现，只要是通过算法实现，就存在一定的规律性和周期性，其结果就可能被预测，所以不是真正意义上的随机数，称为伪随机数。

JavaScript 自带的随机数生成方法是以当前时间为随机数种子，多次取值的结果是均匀分布的（[参考：Math.random() 二三事](https://fed.taobao.org/blog/taofed/do71ct/some-thing-about-random)）。

所以其实可以认为，我们在程序中谈到的随机数都是伪随机数。

## 涉及到的几个基本方法

`Math.random()` 生成一个 **[0, 1)** 的伪随机数

`Math.floor()` 向下取整

`Math.ceil()` 向上取整

`Math.round()` 四舍五入取整

`parseInt()` 向下取整（十进制）

## 问题一：生成一个 [0, n) 的随机整数

通过 `Math.random()` 方法，其实 **[0, 1)** 也属于 **[0, n)**，可以看成 `Math.random() * 1`

`Math.random() * n` 可以得到一个 **[0, n)** 的随机数，然后向下取整即可

方法： `Math.floor(Math.random() * n)`

## 问题二：在 0 和 1 两个数中随机取一个

方法一： `Math.round(Math.random())` 通过四舍五入，因为 `Math.random()` 的结果是均衡分布的，所以这种方法的结果也是均衡分布的

方法二： `Math.ceil(Math.random())` 通过向上取整，显然这种方式得到 0 的概率远远低于得到 1 的概率

## 问题三：生成一个 [0, n] 的随机整数

通过前面两个问题，可以得到以下三种方法

方法一： `Math.floor(Math.random() * (n + 1))`，这种方法的结果是均衡分布的

方法二： `Math.ceil(Math.random() * n)`，这种方法的结果取 0 的概率极低

方法三： `Math.round(Math.random() * n)`，这种方法的结果相对均衡，取最小值 0 和取最大值 n 的概率相对其他结果的概率折半（0 的结果需要随机到 < 0.5，n 的结果需要随机到 >= (n-1).5, 而其他值的随机范围是 (n-2).5 <= x < (n-1).5）)

## 问题四：生成一个 [min, max) 的随机整数

通过求 max 和 min 的差 x 可以得到 [0, x) 范围的数，在这个基础上加上 min 即可得到 [min, x + min) 的数，而 x + min = max

方法： `Math.floor(Math.random() * (max - min)) + min`

## 问题五：生成一个 [min, max] 的随机整数

方法： `Math.floor(Math.random() * (max - min + 1)) + min`
