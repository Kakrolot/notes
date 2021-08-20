## leetcode算法练习

### 2021-07-06

#### 1、二分查找

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length-1;
        while(left<=right){
          //实际使用求中间mid索引建议用这种方法：int mid = left + (right-left)/2; 可以防止left+right溢出（超出整数范围）。
            int mid = left+(right-left)/2;  
            if(target == nums[mid]){
                return mid;
            }else if(target > nums[mid]){
                left=mid+1;
            }else if(target < nums[mid]){
                right=mid-1;
            }
        }
        return -1;
    }
}
```

#### 2、第一个错误版本

```json
#描述
你是产品经理，目前正在带领一个团队开发新的产品。不幸的是，你的产品的最新版本没有通过质量检测。由于每个版本都是基于之前的版本开发的，所以错误的版本之后的所有版本都是错的。

假设你有 n 个版本 [1, 2, ..., n]，你想找出导致之后所有版本出错的第一个错误的版本。

你可以通过调用 bool isBadVersion(version) 接口来判断版本号 version 是否在单元测试中出错。实现一个函数来查找第一个错误的版本。你应该尽量减少对调用 API 的次数


```

**思路:**

因为题目要求尽量减少调用检查接口的次数，所以不能对每个版本都调用检查接口，而是应该将调用检查接口的次数降到最低。

注意到一个性质：当一个版本为正确版本，则该版本之前的所有版本均为正确版本；当一个版本为错误版本，则该版本之后的所有版本均为错误版本。我们可以利用这个性质进行二分查找。

具体地，将左右边界分别初始化为 11 和 nn，其中 nn 是给定的版本数量。设定左右边界之后，每次我们都依据左右边界找到其中间的版本，检查其是否为正确版本。如果该版本为正确版本，那么第一个错误的版本必然位于该版本的右侧，我们缩紧左边界；否则第一个错误的版本必然位于该版本及该版本的左侧，我们缩紧右边界。

这样我们每判断一次都可以缩紧一次边界，而每次缩紧时两边界距离将变为原来的一半，因此我们至多只需要缩紧 O(\log n)O(logn) 次。

**代码**:

```java
public class Solution extends VersionControl {
  //注意版本号 从1开始
    public int firstBadVersion(int n) {
        int left = 1;
        int right = n;
        int mid;
        
        while(left < right){
            mid = left + (right-left)/2;
            if(isBadVersion(mid)){
                right = mid;
            }else{
                left = mid+1;
            }
        }
        return left;
    }
}
```



#### 3、搜索插入位置

**描述**

```html
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。
```

**思路**

利用二分查找

```html
假设题意是叫你在排序数组中寻找是否存在一个目标值，那么训练有素的读者肯定立马就能想到利用二分法在 O(\log n)O(logn) 的时间内找到是否存在目标值。但这题还多了个额外的条件，即如果不存在数组中的时候需要返回按顺序插入的位置，那我们还能用二分法么？答案是可以的，我们只需要稍作修改即可。

考虑这个插入的位置 \textit{pos}pos，它成立的条件为：

\textit{nums}[pos-1]<\textit{target}\le \textit{nums}[pos]
nums[pos−1]<target≤nums[pos]

其中 \textit{nums}nums 代表排序数组。由于如果存在这个目标值，我们返回的索引也是 \textit{pos}pos，因此我们可以将两个条件合并得出最后的目标：「在一个有序数组中找第一个大于等于 \textit{target}target 的下标」。

问题转化到这里，直接套用二分法即可，即不断用二分法逼近查找第一个大于等于 \textit{target}target 的下标 。下文给出的代码是笔者习惯的二分写法，\textit{ans}ans 初值设置为数组长度可以省略边界条件的判断，因为存在一种情况是 \textit{target}target 大于数组中的所有数，此时需要插入到数组长度的位置。

```

**代码：**

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length-1;
        int mid;
        while(left<=right){
            mid = left + (right-left)/2;
            if(nums[mid] == target){
                return mid;
            }else if(nums[mid] < target){
                left = mid+1;
            }else if(nums[mid] > target){
                right = mid-1;
            }
        }
        return left;
    }
}
```

**复杂度分析**

- 时间复杂度：O(\log n)O(logn)，其中 nn 为数组的长度。二分查找所需的时间复杂度为 O(\log n)O(logn)。
- 空间复杂度：O(1)O(1)。我们只需要常数空间存放若干变量。



###  2021-07-07

#### 1.有序数组的平方

**描述：**

给你一个按 **非递减顺序** 排序的整数数组 `nums`，返回 **每个数字的平方** 组成的新数组，要求也按 **非递减顺序** **排序。**

**思路1：**

直接平方然后排序

**代码：**

- 快速排序

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int[] result = new int[nums.length];
        for(int i = 0; i <= nums.length-1; i++){
            result[i] = nums[i] * nums[i];
        }
        quickSort(result,0,result.length-1);
        return result;

    }

private static void quickSort(int[] arr, int low, int high) {

        if (low < high) {
            // 找寻基准数据的正确索引
            int index = getIndex(arr, low, high);

            // 进行迭代对index之前和之后的数组进行相同的操作使整个数组变成有序
            //quickSort(arr, 0, index - 1); 之前的版本，这种姿势有很大的性能问题，谢谢大家的建议
            quickSort(arr, low, index - 1);
            quickSort(arr, index + 1, high);
        }

    }

    private static int getIndex(int[] arr, int low, int high) {
        // 基准数据
        int tmp = arr[low];
        while (low < high) {
            // 当队尾的元素大于等于基准数据时,向前挪动high指针
            while (low < high && arr[high] >= tmp) {
                high--;
            }
            // 如果队尾元素小于tmp了,需要将其赋值给low
            arr[low] = arr[high];
            // 当队首元素小于等于tmp时,向前挪动low指针
            while (low < high && arr[low] <= tmp) {
                low++;
            }
            // 当队首元素大于tmp时,需要将其赋值给high
            arr[high] = arr[low];

        }
        // 跳出循环时low和high相等,此时的low或high就是tmp的正确索引位置
        // 由原理部分可以很清楚的知道low位置的值并不是tmp,所以需要将tmp赋值给arr[low]
        arr[low] = tmp;
        return low; // 返回tmp的正确位置
    }

}
```

- Arrays.sort接口

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int[] result = new int[nums.length];
        for(int i = 0; i <= nums.length-1; i++){
            result[i] = nums[i] * nums[i];
        }
        Arrays.sort(result,0,result.length-1);
        return result;

    }
}
```

- 双指针算法

```java
class Solution {
    public  static  int[] sortedSquares(int[] nums) {
            int n = nums.length;
            int negative = -1;
            for (int i = 0; i < n; ++i) {
                if (nums[i] < 0) {
                    negative = i;
                } else {
                    break;
                }
            }

            int[] ans = new int[n];
            int index = 0, i = negative, j = negative + 1;
            while (i >= 0 || j < n) {
                if (i < 0) {
                    ans[index] = nums[j] * nums[j];
                    ++j;
                } else if (j == n) {
                    ans[index] = nums[i] * nums[i];
                    --i;
                } else if (nums[i] * nums[i] < nums[j] * nums[j]) {
                    ans[index] = nums[i] * nums[i];
                    --i;
                } else {
                    ans[index] = nums[j] * nums[j];
                    ++j;
                }
                ++index;
            }

            return ans;
        }
}
```

#### 2.旋转数组

**描述：**

给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。

 

进阶：

尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。
你可以使用空间复杂度为 O(1) 的 原地 算法解决这个问题吗？

```html
输入: nums = [1,2,3,4,5,6,7], k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]

来源：力扣（LeetCode）
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

链接：https://leetcode-cn.com/problems/rotate-array



**思路：**

1.使用额外的数组

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        int[] newArr = new int[n];
        for (int i = 0; i < n; ++i) {
            newArr[(i + k) % n] = nums[i];
        }
        System.arraycopy(newArr, 0, nums, 0, n);
    }
}
```

**其他方法参考：**

https://leetcode-cn.com/problems/rotate-array/solution/xuan-zhuan-shu-zu-by-leetcode-solution-nipk/

 2.多次翻转

```java
class Solution {
    public void rotate(int[] nums, int k) {
        k %= nums.length;
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }
    public void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start += 1;
            end -= 1;
        }
    }
}

```

#### 3.存在重复元素

**描述：**

给定一个整数数组，判断是否存在重复元素。

如果存在一值在数组中出现至少两次，函数返回 `true` 。如果数组中每个元素都不相同，则返回 `false` 。

```java

//先排序 然后前后比对
class Solution {
    public boolean containsDuplicate(int[] nums) {
        //先排序 
        Arrays.sort(nums);
        for(int i=0;i<nums.length-1; i++){
            if(nums[i] == nums [i+1]){
                return true;
            }
        }
        return false;
    }
}
```

## 2021-07-08

#### 1.移动0，将数组中的0 移动到最后

**说明**

1. 必须在原数组上操作，不能拷贝额外的数组。
2. 尽量减少操作次数。

**思路**

利用双指针 在一个数组上进行交换操作

```java
class Solution {
    public static void moveZeroes(int[] nums) {
        if(nums.length == 1){
            return;
        }
        int low = 0;
        int high = 1;
        int temp;
        while(low <= high ){
            if(nums[low] != 0){
                low++;
                high++;
            }else if(nums[low] == 0 && nums[high] != 0){
                temp = nums[low];
                nums[low] = nums[high];
                nums[high] = temp;
                low++;
                high++;
            }else if(nums[low] == 0 && nums[high] == 0 ){
                high ++;
            }

            if(high == nums.length){
                break;
            }
        }
    }
}
```



## 2021-07-12

### 1.反转字符串

**描述**

编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 char[] 的形式给出。

不要给另外的数组分配额外的空间，你必须原地修改输入数组、使用 O(1) 的额外空间解决这一问题。

你可以假设数组中的所有字符都是 ASCII 码表中的可打印字符。

**思路**

利用双指针 前后交换

```html
输入：["h","e","l","l","o"]
输出：["o","l","l","e","h"]
```



### 2.反转字符串中的单词

**描述**

给定一个字符串，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

**思路**

遇到空格时 标记

获取单词头与单词尾巴的下标

进行转换 

**代码**

```java
class Solution {
    public String reverseWords(String s) {
        StringBuffer res = new StringBuffer();
        int length = s.length();
        int i = 0;
        while (i < s.length()) {
            int start = i;
            while (i < s.length() && s.charAt(i) != ' ') {
                i++;
            }
            for (int j = start; j < i; j++) {
              //注意是从最后一个值得前一位  最后一位位空格
                res.append(s.charAt(start+i-1-j));
            }
            if (i++ != s.length()) {
                res.append(" ");
            }
        }
        return res.toString();
    }
}
```



## 2021-07-13

#### 1.链表的中间节点

**描述**

给定一个头结点为 `head` 的非空单链表，返回链表的中间结点。

如果有两个中间结点，则返回第二个中间结点。



**思路**

快慢双指针，第一个每次走一步 next   

第二个每次走两个 next.next；

当第二个走完是 第一个指针恰好走到一般 输出则为中间节点

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode p = head;
        ListNode q = head;
        while(q != null && q.next!=null){
            p = p.next;
            q = q.next.next;
        }
        return p;
    }
}
```

**其他思路**

数组，开辟一个新的数组内存空间 将链表的每段值放入对应的数组下标中

最后拿中间下标的值



```java
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode[] A = new ListNode[100];
        int t = 0;
        while (head != null) {
            A[t++] = head;
            head = head.next;
        }
        return A[t / 2];
    }
}


```



单指针法 

先遍历完一遍链表

记录链表节点个数 n

然后循环 n/2 次 输出节点

```java
class Solution {
    public ListNode middleNode(ListNode head) {
        int n = 0;
        ListNode cur = head;
        while (cur != null) {
            ++n;
            cur = cur.next;
        }
        int k = 0;
        cur = head;
        while (k < n / 2) {
            ++k;
            cur = cur.next;
        }
        return cur;
    }
}


```



### 2.删除倒数第n个节点

```java
  public ListNode removeNthFromEnd(ListNode head, int n) {    
        ListNode pre = new ListNode(0);
        pre.next = head;
        ListNode start = pre, end = pre;
        while(n != 0) {
            start = start.next;
            n--;
        }
        while(start.next != null) {
            start = start.next;
            end = end.next;
        }
        end.next = end.next.next;
        return pre.next;
    }
```

