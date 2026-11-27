# Maximum Strong Pair XOR II

| Field | Value |
|-------|-------|
| **Platform** | LeetCode |
| **Difficulty** | Hard |
| **Language** | cpp |
| **Solved On** | November 27, 2026 |
| **Tags** | Array, Hash Table, Bit Manipulation, Trie, Sliding Window |
| **Link** | [View Problem](https://leetcode.com/problems/maximum-strong-pair-xor-ii/) |
| **Runtime** | 353 ms |
| **Memory** | 172.1 MB |

## Problem Description

<p>You are given a <strong>0-indexed</strong> integer array <code>nums</code>. A pair of integers <code>x</code> and <code>y</code> is called a <strong>strong</strong> pair if it satisfies the condition:</p>

<ul>
	<li><code>|x - y| &lt;= min(x, y)</code></li>
</ul>

<p>You need to select two integers from <code>nums</code> such that they form a strong pair and their bitwise <code>XOR</code> is the <strong>maximum</strong> among all strong pairs in the array.</p>

<p>Return <em>the <strong>maximum</strong> </em><code>XOR</code><em> value out of all possible strong pairs in the array</em> <code>nums</code>.</p>

<p><strong>Note</strong> that you can pick the same integer twice to form a pair.</p>

<p>&nbsp;</p>
<p><span class="float-right -my-0.5 ml-2 inline-flex select-none items-center" data-example-lang-controls=""><span role="group" class="inline-flex h-6 items-center rounded-sd-md bg-sd-muted p-0.5" data-example-lang-toggle=""><button type="button" aria-pressed="true" class="h-5 max-w-[10rem] truncate whitespace-nowrap rounded-sd-sm border px-2 text-xs font-normal leading-none border-sd-border bg-sd-background text-sd-foreground">Original</button><button type="button" aria-pressed="false" class="h-5 max-w-[10rem] truncate whitespace-nowrap rounded-sd-sm border px-2 text-xs font-normal leading-none border-transparent text-sd-muted-foreground hover:text-sd-foreground">C++</button></span></span><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,2,3,4,5]
<strong>Output:</strong> 7
<strong>Explanation:</strong> There are 11 strong pairs in the array <code>nums</code>: (1, 1), (1, 2), (2, 2), (2, 3), (2, 4), (3, 3), (3, 4), (3, 5), (4, 4), (4, 5) and (5, 5).
The maximum XOR possible from these pairs is 3 XOR 4 = 7.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [10,100]
<strong>Output:</strong> 0
<strong>Explanation:</strong> There are 2 strong pairs in the array nums: (10, 10) and (100, 100).
The maximum XOR possible from these pairs is 10 XOR 10 = 0 since the pair (100, 100) also gives 100 XOR 100 = 0.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> nums = [500,520,2500,3000]
<strong>Output:</strong> 1020
<strong>Explanation:</strong> There are 6 strong pairs in the array nums: (500, 500), (500, 520), (520, 520), (2500, 2500), (2500, 3000) and (3000, 3000).
The maximum XOR possible from these pairs is 500 XOR 520 = 1020 since the only other non-zero XOR value is 2500 XOR 3000 = 636.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>1 &lt;= nums[i] &lt;= 2<sup>20</sup> - 1</code></li>
</ul>


##  Top Community Optimal Approach

<details>
<summary>Click to expand</summary>

**Title**: Concise Binary Search || C++
**Author**: [@JakevK](https://leetcode.com/JakevK/)
**Upvotes**: 16 👍
**Link**: [View Original Post](https://leetcode.com/problems/maximum-strong-pair-xor-ii/solutions/4278127/)

---

No need for a trie - just do a whole lotta binary searching.
```
class Solution {
public:
    int bsearch(vector<int>& nums, int l, int r, int mask) {
        // Return min index i (l <= i < r), such that (nums[i] & mask) != 0
        while (l < r) {
            int mid = (l+r) / 2;
            if (mask & nums[mid]) r = mid;
            else l = mid+1;
        }
        return l;
    }
    
    int maximumStrongPairXor(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int ans = 0;
        
        for (int i = 0; i < nums.size(); ++i) {
            int l = i, r = upper_bound(nums.begin(), nums.end(), nums[i]*2) - nums.begin();
            
            for (int mask = 1 << 20; mask; mask >>= 1) {
                int nl = l, nr = r;
                ((mask & nums[i]) ? nr : nl) = bsearch(nums, l, r, mask);
                if (nl != nr) l = nl, r = nr;
            }
            
            ans = max(ans, nums[i] ^ nums[l]);
        }
        
        return ans;
    }
};
```

</details>
