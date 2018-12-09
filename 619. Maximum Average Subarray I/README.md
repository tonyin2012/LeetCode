这道题虽然是求平均数，但可以视为求和。且已经规定了连续数组，那么就完全可以想像成一个长度为 k 的滑块。从头滑到尾，统计一下最大那个和就好了。

所以最常规的思路就是先求出滑块的初始和：

```cpp
double sum = 0.0;
for (int i = 0; i != k; ++i) {
  sum += nums[i];
}
```

然后滑块开始滑动，滑动的过程可以理解为，去头接尾：

```cpp
for (int i = 1; i + k <= nums.size(); ++i) {
  sum += nums[i+k-1] - nums[i-1];
}
```

然后另设一个变量，如 max_sum 来统计最大的 sum 即可。

----

稍微 trick 一点的改进呢，就是把滑块想像成一个蠕虫。蠕虫拱起来的最高点就是它前进的标志。那么在这个问题里，我们最关心的就是求和这个过程，所以可以把这个最高点视为求和。

那么蠕虫向前移动的步骤，就是不断累加和的过程，但吞一口，必须得拉一次，这个别忘了。