快速排序算法
-------------
> 快速排序（Quicksort）是对冒泡排序的一种改进。 快速排序由C. A. R.
> Hoare在1962年提出。它的基本思想是：通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。


算法介绍
-------------

设要排序的数组是A[0]……A[N-1]，首先任意选取一个数据（通常选用数组的第一个数）作为关键数据，然后将所有比它小的数都放到它前面，所有比它大的数都放到它后面，这个过程称为一趟快速排序。值得注意的是，快速排序不是一种稳定的排序算法，也就是说，多个相同的值的相对位置也许会在算法结束时产生变动。
一趟快速排序的算法是：
1）设置两个变量i、j，排序开始的时候：i=0，j=N-1；
2）以第一个数组元素作为关键数据，赋值给key，即key=A[0]；
3）从j开始向前搜索，即由后开始向前搜索(j--)，找到第一个小于key的值A[j]，将A[j]和A[i]互换；
4）从i开始向后搜索，即由前开始向后搜索(i++)，找到第一个大于key的A[i]，将A[i]和A[j]互换；
5）重复第3、4步，直到i=j； (3,4步中，没找到符合条件的值，即3中A[j]不小于key,4中A[i]不大于key的时候改变j、i的值，使得j=j-1，i=i+1，直至找到为止。找到符合条件的值，进行交换的时候i， j指针位置不变。另外，i==j这一过程一定正好是i+或j-完成的时候，此时令循环结束）。


代码演示:
-------------
```c
void sort(int *a, int left, int right)
{
    if(left >= right)/*如果左边索引大于或者等于右边的索引就代表已经整理完成一个组了*/
    {
        return ;
    }
    int i = left;
    int j = right;
    int key = a[left];
    while(i < j) /*控制在当组内寻找一遍*/
    {
        while(i < j && key <= a[j])
        /*而寻找结束的条件就是，1，找到一个小于或者大于key的数（大于或小于取决于你想升
        序还是降序）2，没有符合条件1的，并且i与j的大小没有反转*/ 
        {
            j--;/*向前寻找*/
        }
        a[i] = a[j];
        /*找到一个这样的数后就把它赋给前面的被拿走的i的值（如果第一次循环且key是
        a[left]，那么就是给key）*/
        while(i < j && key >= a[i])
        /*这是i在当组内向前寻找，同上，不过注意与key的大小关系停止循环和上面相反，
        因为排序思想是把数往两边扔，所以左右两边的数大小与key的关系相反*/
        {
            i++;
        }
        a[j] = a[i];
    }
    a[i] = key;/*当在当组内找完一遍以后就把中间数key回归*/
    sort(a, left, i - 1);/*最后用同样的方式对分出来的左边的小组进行同上的做法*/
    sort(a, i + 1, right);/*用同样的方式对分出来的右边的小组进行同上的做法*/
    /*当然最后可能会出现很多分左右，直到每一组的i = j 为止*/
}
```
