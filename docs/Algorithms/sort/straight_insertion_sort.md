---
comments: true
---

直接插入排序（Straight Insertion Sort）是一种最简单的排序方法，其基本操作是将一条记录插入到已排好的有序表中，从而得到一个新的、记录数量增 1 的有序表。[^1]

## 一、实现思路

### 1.1 步骤

- [ ] 将整个数组分组两部分，左边和右边部分；
- [ ] 在排序的过程中，无需管右边部分的顺序，只需要保证左边始终有序；
- [ ] 遍历从左到右，每遍历到一个新的元素，都将其取出(1)；
    { .annotate}

    1.  因为无法马上确定其位置

- [ ] 然后在保证顺序的左边部分中寻找其应该的位置；
- [ ] 即，从该元素位置向左遍历，并判断是否应该插入；
- [ ] 如不能插入，则将判断的元素向右移位，反之插入；
- [ ] 如此反复直至遍历完成，那么整个数组都是有序的了。

### 1.2 流程图

暂无

## 二、实现代码

### 2.1 多语言版本

推荐学习 C++ 版本，更利于理解算法的本质。另外，下面 Python 的实现方式与其它三个略微有些不同，请注意。

=== "👍 C 17"

    ```C
    --8<-- "sources/Algorithms/sort/C/straight_insertion_sort.c"
    ```

    1. 相等时，被比较元素原来在前面的就不用右移了，保证稳定性
    
=== "⚡ C++ 20"

    ```C++
    --8<-- "sources/Algorithms/sort/C++/straight_insertion_sort.cpp"
    ```

    1. 相等时，被比较元素原来在前面的就不用右移了，保证稳定性
    
=== "🐍 Python 3.12"

    ```Python
    --8<-- "sources/Algorithms/sort/Python/straight_insertion_sort.py"
    ```

    1. 相等时，不确定位置的元素的位置也能确定了，一定在当前被比较元素的右边

    !!! Tip "提示"
        若要实现 C/C++ 那样，通过参数 n 只排序前几个元素的话，可采用对列表切片引用的方式传参，可达到相同效果。

=== "☕ Java 21"

    ```Java
    --8<-- "sources/Algorithms/sort/Java/straight_insertion_sort.java"
    ```

    1. 相等时，被比较元素原来在前面的就不用右移了，保证稳定性

### 2.2 测试用例

=== "输入"
    
    ```text
    9
    6 28 13 72 85 39 41 6 20
    ```

=== "输出"

    ```text
    6 6 13 20 28 39 41 72 85
    ```

### 2.3 相关习题

暂无

## 三、算法性质

### 3.1 时空复杂度

|   复杂度   |         😀最好情况          |          😭最坏情况           | 🫤平均情况 |
| :--------: | :------------------------: | :--------------------------: | :-------: |
| 时间复杂度 | $O(n)${ title="数组顺序" } | $O(n^2)${ title="数组逆序" } | $O(n^2)$  |
| 空间复杂度 |           $O(1)$           |            $O(1)$            |  $O(1)$   |

#### 3.1.1 时间复杂度分析

有一个大循环从左边第 2 个元素(1)开始到右边遍历了数组的每一个元素，即 n-1 个元素被大循环遍历，在每一个小循环中，该元素会反向对左边已遍历（排好序）的元素进行再次遍历，遍历 i-1 次。但每次小循环会在元素插入的时候终止，我们并不知道是在什么时候终止的，但我们知道，这是随机的（取决于数据）。
{ .annotate }

1. 第 1 个元素本身就是有序的，遍历它没有什么意义，直接跳过

当数组初始为顺序时，每个小循环只需要遍历 1 次，反之，当数组逆序的时候，就需要完成全部的遍历过程，即每次小循环要遍历 i-1 次，平均下来，每次小循环遍历 (i-1)/2 次，因此时间复杂度：

数组顺序时的最好情况：

$$
O(T_n) = O(1 + 1 + 1 + ... + 1) = O(n-1) = O(n)
$$

数组逆序时的最坏情况：

$$
O(T_n) = O(1 + 2 + 3 + ... + (n-1)) = O\Big(\frac{n(n-1)}{2}\Big) = O(n^2)
$$

平均情况：

$$
O(T_n) = O\Big(\frac{1}{2} + \frac{2}{2} + \frac{3}{2} + ... + \frac{n-1}{2}\Big) = O\Big(\frac{n(n-1)}{4}\Big) = O(n^2)
$$

#### 3.1.2 空间复杂度分析

整个算法的过程中，我们只用了 1 个临时变量来存储被取出来的那个元素，因此空间复杂度：

$$
O(S_n) = O(1)
$$

### 3.2 稳定性与排序方式

|     算法     |  稳定性  | 排序方式 |
| :----------: | :------: | :------: |
| 直接插入排序 | 可以稳定 | 内部排序 |

#### 3.2.1 稳定性分析

能否稳定取决于具体的实现，实现细节没把握好也可能导致不稳定。关键在于对元素比较出现相等情况时是否应该插入的判断。

#### 3.2.2 排序方式分析

排序方式属于内部排序，没有用到外部的空间。

## 四、参考资料

[^1]: [直接插入排序 · 百度百科](https://baike.baidu.com/item/%E7%9B%B4%E6%8E%A5%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F/8255911)