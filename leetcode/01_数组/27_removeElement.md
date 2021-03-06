# 27_移除元素, Easy
> 给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。

> 不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。

> 元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

> 示例 1:

> 给定 nums = [3,2,2,3], val = 3,
> 函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。

> 你不需要考虑数组中超出新长度后面的元素。

> 示例 2:

> 给定 nums = [0,1,2,2,3,0,4,2], val = 2,
> 函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。

> 注意这五个元素可为任意顺序。

> 你不需要考虑数组中超出新长度后面的元素。

## 解法1: 双指针, 直接赋值
``` cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        if(nums.size() == 0)// 如果空, 直接返回
        {
            return 0;
        }
        int i = 0;
        for(int j = 0; j < nums.size(); j++)
        {
            if(nums.at(j) != val)
            {
                nums.at(i) = nums.at(j);// 如果不是val, 就直接放到原数组中
                i++;
            }
        }
        return i;
    }
};
```

## 解法2: 双指针, 交换赋值
- 解法1在有些情况下会有重复操作
	1.  [1, 2, 3, 4, 5], val = 6, 其实是什么都不用做的, 但是解法1复制了5次(或者判断了5次)
	2.  [4, 1, 2, 3, 5], val = 4, 解法1在扣掉4以后, 需要把后面的数都往前移动1次
- 利用题目中**元素顺序可以改变的条件**, 情况2时, 可以直接把4和最末尾的5交换, 这样只需一次交换操作即可
``` cpp
int length = nums.size(); // 待遍历数组的长度
int j = 0;
while(j < length)
{
    if(nums.at(j) == val)
    {
        nums.at(j) = nums.at(length - 1); // 把待遍历数组最后一位放到前面来
        // nums.at(length - 1) = val; // 实际上并不用真的做交换, 反正也不用了
        length--; // 当把重复值放到最后以后, 相当于待遍历的数组少了最后一位,即,长度减一
    }
    else
    {
        j++;
    }
}
return j;
```

## 小结
- 解法2与解法1相比, 都需要遍历整个数组, 也就是O(n), 区别在于解法1操作不同与val的值, 而解法2操作与val相同的值
- 因此:
	- 当输入数组中val值比较少时, 解法2 的操作较少
	- 而当val值比较多时, 解法1 的操作数较少
