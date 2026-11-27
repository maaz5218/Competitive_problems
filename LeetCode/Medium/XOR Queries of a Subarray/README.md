# XOR Queries of a Subarray

| Field | Value |
|-------|-------|
| **Platform** | LeetCode |
| **Difficulty** | Medium |
| **Language** | cpp |
| **Solved On** | November 27, 2026 |
| **Tags** | Array, Bit Manipulation, Prefix Sum |
| **Link** | [View Problem](https://leetcode.com/problems/xor-queries-of-a-subarray/) |
| **Runtime** | 3 ms |
| **Memory** | 91.2 MB |

## Problem Description

<p>You are given an array <code>arr</code> of positive integers. You are also given the array <code>queries</code> where <code>queries[i] = [left<sub>i, </sub>right<sub>i</sub>]</code>.</p>

<p>For each query <code>i</code> compute the <strong>XOR</strong> of elements from <code>left<sub>i</sub></code> to <code>right<sub>i</sub></code> (that is, <code>arr[left<sub>i</sub>] XOR arr[left<sub>i</sub> + 1] XOR ... XOR arr[right<sub>i</sub>]</code> ).</p>

<p>Return an array <code>answer</code> where <code>answer[i]</code> is the answer to the <code>i<sup>th</sup></code> query.</p>

<p>&nbsp;</p>
<p><span class="float-right -my-0.5 ml-2 inline-flex select-none items-center" data-example-lang-controls=""><span role="group" class="inline-flex h-6 items-center rounded-sd-md bg-sd-muted p-0.5" data-example-lang-toggle=""><button type="button" aria-pressed="true" class="h-5 max-w-[10rem] truncate whitespace-nowrap rounded-sd-sm border px-2 text-xs font-normal leading-none border-sd-border bg-sd-background text-sd-foreground">Original</button><button type="button" aria-pressed="false" class="h-5 max-w-[10rem] truncate whitespace-nowrap rounded-sd-sm border px-2 text-xs font-normal leading-none border-transparent text-sd-muted-foreground hover:text-sd-foreground">C++</button></span></span><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> arr = [1,3,4,8], queries = [[0,1],[1,2],[0,3],[3,3]]
<strong>Output:</strong> [2,7,14,8] 
<strong>Explanation:</strong> 
The binary representation of the elements in the array are:
1 = 0001 
3 = 0011 
4 = 0100 
8 = 1000 
The XOR values for queries are:
[0,1] = 1 xor 3 = 2 
[1,2] = 3 xor 4 = 7 
[0,3] = 1 xor 3 xor 4 xor 8 = 14 
[3,3] = 8
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> arr = [4,8,2,10], queries = [[2,3],[1,3],[0,0],[0,3]]
<strong>Output:</strong> [8,0,4,4]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= arr.length, queries.length &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>1 &lt;= arr[i] &lt;= 10<sup>9</sup></code></li>
	<li><code>queries[i].length == 2</code></li>
	<li><code>0 &lt;= left<sub>i</sub> &lt;= right<sub>i</sub> &lt; arr.length</code></li>
</ul>


##  Top Community Optimal Approach

<details>
<summary>Click to expand</summary>

**Title**: ✅Beats 100% -Explained with [ Video ] -C++/Java/Python/JS - Prefix XOR- Explained in Detail
**Author**: [@lancertech6](https://leetcode.com/lancertech6/)
**Upvotes**: 133 👍
**Link**: [View Original Post](https://leetcode.com/problems/xor-queries-of-a-subarray/solutions/5778700/)

---

![Screenshot 2024-09-13 070037.png](https://assets.leetcode.com/users/images/fe7c65aa-e528-4540-9fc0-cb0707f5a85c_1726191451.4362981.png)

# YouTube Video Explanation:

### To watch the video please click on "Watch On Youtube" option  available the left bottom corner of the thumbnail.

<!-- **If you want a video for this question please write in the comments** -->


https://youtu.be/neLRg9AzV_U


**\uD83D\uDD25 Please like, share, and subscribe to support our channel\'s mission of making complex concepts easy to understand.**

Subscribe Link: https://www.youtube.com/@leetlogics/?sub_confirmation=1

*Subscribe Goal: 2900 Subscribers*
*Current Subscribers: 2831*

Follow me on Instagram : https://www.instagram.com/divyansh.nishad/

---

# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
To solve the problem efficiently, we need to calculate the XOR of subarrays for multiple queries. Calculating the XOR for each subarray directly for every query can be slow and inefficient, especially with the given constraints. Instead, we use a preprocessing step to make the query responses faster.

# Approach
<!-- Describe your approach to solving the problem. -->
1. **Preprocessing with Prefix XOR Array**:
   - We first compute a prefix XOR array `pre`, where `pre[i]` is the XOR of all elements from the start of the array up to index `i`. This allows us to quickly compute the XOR for any subarray.

2. **Compute XOR for Queries**:
   - Given the prefix XOR array, for any query that asks for the XOR of the subarray from index `lefti` to `righti`, we can efficiently compute the result using:
     - `pre[righti]` if `lefti` is 0.
     - `pre[righti] ^ pre[lefti - 1]` otherwise. This is because `pre[righti]` gives the XOR from the start of the array up to `righti`, and subtracting `pre[lefti - 1]` removes the contribution of the elements before `lefti`.


# Step-by-Step Explanation

Let\'s use the following arrays and queries:

- **Array (`arr`)**: `[1, 3, 4, 8]`
- **Queries**: `[[0, 1], [1, 2], [0, 3], [3, 3]]`


#### 1. Compute Prefix XOR Array

First, we compute the prefix XOR array (`pre`). This array helps us quickly compute the XOR of any subarray.

**Initial Array**: `[1, 3, 4, 8]`

| Index `i` | `arr[i]` | `pre[i]`        | Explanation                            |
|-----------|----------|-----------------|----------------------------------------|
| 0         | 1        | 1               | `pre[0] = arr[0] = 1`                  |
| 1         | 3        | `1 ^ 3 = 2`     | `pre[1] = pre[0] ^ arr[1] = 1 ^ 3`    |
| 2         | 4        | `2 ^ 4 = 6`     | `pre[2] = pre[1] ^ arr[2] = 2 ^ 4`    |
| 3         | 8        | `6 ^ 8 = 14`    | `pre[3] = pre[2] ^ arr[3] = 6 ^ 8`    |

So the prefix XOR array is: `[1, 2, 6, 14]`.

#### 2. Answer Queries Using Prefix XOR Array

Now, using the prefix XOR array, we can quickly answer each query.

**Queries**: `[[0, 1], [1, 2], [0, 3], [3, 3]]`

For each query `[left, right]`, we calculate:

- If `left == 0`: The result is `pre[right]`.
- Otherwise: The result is `pre[right] ^ pre[left - 1]`.

| Query     | `left` | `right` | Calculation                         | Result |
|-----------|--------|---------|-------------------------------------|--------|
| `[0, 1]`  | 0      | 1       | `pre[1] = 2`                         | 2      |
| `[1, 2]`  | 1      | 2       | `pre[2] ^ pre[0] = 6 ^ 1 = 7`       | 7      |
| `[0, 3]`  | 0      | 3       | `pre[3] = 14`                        | 14     |
| `[3, 3]`  | 3      | 3       | `pre[3] ^ pre[2] = 14 ^ 6 = 8`      | 8      |


### Explanation

1. **Prefix XOR Array**: This array helps to quickly compute the XOR of any subarray. The value at each index `i` in `pre` represents the XOR of all elements from the start of the array to index `i`.

2. **Query Resolution**: For each query `[left, right]`:
   - If `left` is 0, the result is simply `pre[right]` because it represents the XOR from the start to `right`.
   - If `left` is not 0, we need to exclude the part of the array before `left`. This is done by XORing `pre[right]` with `pre[left - 1]`, which removes the XOR of elements before `left`.


# Complexity
- **Time Complexity**:
  - **Preprocessing**: Building the prefix XOR array takes (O(n)), where (n) is the length of the input array.
  - **Query Processing**: Each query is processed in constant time (O(1)) using the precomputed prefix XOR array.
  - Overall, the time complexity is (O(n + q)), where (q) is the number of queries. This is efficient given the constraints.

- **Space Complexity**:
  - **Prefix XOR Array**: Requires (O(n)) space.
  - **Result Array**: Requires (O(q)) space.
  - Overall, the space complexity is (O(n + q)), which is manageable within the given constraints.


# Code
```java []
class Solution {
    public int[] xorQueries(int[] arr, int[][] queries) {
        int n=arr.length;
        int[] pre=new int[n];
        pre[0]=arr[0];
        for(int i=1;i<n;i++) {
            pre[i]=pre[i-1]^arr[i];
        }
        int[] res=new int[queries.length];
        for(int k=0;k<queries.length;k++) {
            int i=queries[k][0];
            int j=queries[k][1];
            if(i==0) {
                res[k]=pre[j];
            } else {
                res[k]=pre[j]^pre[i-1];
            }
        }
        return res;
    }
}
```
```C++ []
class Solution {
public:
    vector<int> xorQueries(vector<int>& arr, vector<vector<int>>& queries) {
        int n = arr.size();
        vector<int> pre(n);
        pre[0] = arr[0];
        
        // Compute prefix XOR array
        for (int i = 1; i < n; ++i) {
            pre[i] = pre[i - 1] ^ arr[i];
        }
        
        std::vector<int> res(queries.size());
        
        // Answer each query
        for (int k = 0; k < queries.size(); ++k) {
            int i = queries[k][0];
            int j = queries[k][1];
            if (i == 0) {
                res[k] = pre[j];
            } else {
                res[k] = pre[j] ^ pre[i - 1];
            }
        }
        
        return res;
    }
};
```
```Python []
class Solution(object):
    def xorQueries(self, arr, queries):
        n = len(arr)
        pre = [0] * n
        pre[0] = arr[0]
        
        # Compute prefix XOR array
        for i in range(1, n):
            pre[i] = pre[i - 1] ^ arr[i]
        
        res = []
        
        # Answer each query
        for left, right in queries:
            if left == 0:
                res.append(pre[right])
            else:
                res.append(pre[right] ^ pre[left - 1])
        
        return res
        
```
```JavaScript []
/**
 * @param {number[]} arr
 * @param {number[][]} queries
 * @return {number[]}
 */
var xorQueries = function(arr, queries) {
    const n = arr.length;
    const pre = new Array(n);
    pre[0] = arr[0];
    
    // Compute prefix XOR array
    for (let i = 1; i < n; i++) {
        pre[i] = pre[i - 1] ^ arr[i];
    }
    
    const res = [];
    
    // Answer each query
    for (const [left, right] of queries) {
        if (left === 0) {
            res.push(pre[right]);
        } else {
            res.push(pre[right] ^ pre[left - 1]);
        }
    }
    
    return res;
};
```

![upvote.png](https://assets.leetcode.com/users/images/6a9faa06-9e71-486e-bdc4-be2e572be61d_1726191431.4196894.png)


</details>
