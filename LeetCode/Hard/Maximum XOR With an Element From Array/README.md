# Maximum XOR With an Element From Array

| Field | Value |
|-------|-------|
| **Platform** | LeetCode |
| **Difficulty** | Hard |
| **Language** | cpp |
| **Solved On** | November 27, 2026 |
| **Tags** | Array, Bit Manipulation, Trie |
| **Link** | [View Problem](https://leetcode.com/problems/maximum-xor-with-an-element-from-array/) |
| **Runtime** | 463 ms |
| **Memory** | 281.9 MB |

## Problem Description

<p>You are given an array <code>nums</code> consisting of non-negative integers. You are also given a <code>queries</code> array, where <code>queries[i] = [x<sub>i</sub>, m<sub>i</sub>]</code>.</p>

<p>The answer to the <code>i<sup>th</sup></code> query is the maximum bitwise <code>XOR</code> value of <code>x<sub>i</sub></code> and any element of <code>nums</code> that does not exceed <code>m<sub>i</sub></code>. In other words, the answer is <code>max(nums[j] XOR x<sub>i</sub>)</code> for all <code>j</code> such that <code>nums[j] &lt;= m<sub>i</sub></code>. If all elements in <code>nums</code> are larger than <code>m<sub>i</sub></code>, then the answer is <code>-1</code>.</p>

<p>Return <em>an integer array </em><code>answer</code><em> where </em><code>answer.length == queries.length</code><em> and </em><code>answer[i]</code><em> is the answer to the </em><code>i<sup>th</sup></code><em> query.</em></p>

<p>&nbsp;</p>
<p><span class="float-right -my-0.5 ml-2 inline-flex select-none items-center" data-example-lang-controls=""><span role="group" class="inline-flex h-6 items-center rounded-sd-md bg-sd-muted p-0.5" data-example-lang-toggle=""><button type="button" aria-pressed="true" class="h-5 max-w-[10rem] truncate whitespace-nowrap rounded-sd-sm border px-2 text-xs font-normal leading-none border-sd-border bg-sd-background text-sd-foreground">Original</button><button type="button" aria-pressed="false" class="h-5 max-w-[10rem] truncate whitespace-nowrap rounded-sd-sm border px-2 text-xs font-normal leading-none border-transparent text-sd-muted-foreground hover:text-sd-foreground">C++</button></span></span><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [0,1,2,3,4], queries = [[3,1],[1,3],[5,6]]
<strong>Output:</strong> [3,3,7]
<strong>Explanation:</strong>
1) 0 and 1 are the only two integers not greater than 1. 0 XOR 3 = 3 and 1 XOR 3 = 2. The larger of the two is 3.
2) 1 XOR 2 = 3.
3) 5 XOR 2 = 7.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [5,2,4,6,6,3], queries = [[12,4],[8,1],[6,3]]
<strong>Output:</strong> [15,-1,5]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length, queries.length &lt;= 10<sup>5</sup></code></li>
	<li><code>queries[i].length == 2</code></li>
	<li><code>0 &lt;= nums[j], x<sub>i</sub>, m<sub>i</sub> &lt;= 10<sup>9</sup></code></li>
</ul>


##  Top Community Optimal Approach

<details>
<summary>Click to expand</summary>

**Title**: Simple and Clean Code || Trie
**Author**: [@Karanveer__Singh](https://leetcode.com/Karanveer__Singh/)
**Upvotes**: 7 👍
**Link**: [View Original Post](https://leetcode.com/problems/maximum-xor-with-an-element-from-array/solutions/1910287/)

---

```
class Node {
private:
    Node *links[2];

public:
    bool containsKey(int bit) {
        return (links[bit] != NULL);
    }

    Node *get(int bit) {
        return links[bit];
    }

    void put(int bit, Node *node) {
        links[bit] = node;
    }
};

class Trie {
private:
    Node *root;

public:
    Trie() {
        root = new Node();
    }

    void insert(int num) {
        Node *node = root;
        for (int i = 31; i >= 0; i--) {
            int bit = (num >> i) & 1;
            if (!node->containsKey(bit)) {
                node->put(bit, new Node());
            }
            node = node->get(bit);
        }
    }

    int getMax(int num) {
        Node *node = root;
        int maxNum = 0;
        for (int i = 31; i >= 0; i--) {
            int bit = (num >> i) & 1;
            if (node->containsKey(1 - bit)) {
                maxNum = maxNum | (1 << i);
                node = node->get(1 - bit);
            }
            else {
                node = node->get(bit);
            }
        }
        return maxNum;
    }
};

class Solution {
public:
    vector<int> maximizeXor(vector<int>& nums, vector<vector<int>>& queries) {
        sort(nums.begin(), nums.end());
        vector<pair<int, pair<int, int> > > offlineQueries;
        vector<int> ans(queries.size(), 0);

        for (int i = 0; i < queries.size(); i++)
            offlineQueries.push_back({queries[i][1], {queries[i][0], i}});

        sort(offlineQueries.begin(), offlineQueries.end());

        int i = 0, n = nums.size();
        Trie t;

        for (int k = 0; k < queries.size(); k++) {
            int ai = offlineQueries[k].first;
            int xi = offlineQueries[k].second.first;
            int qIndx = offlineQueries[k].second.second;

            while (i < n && nums[i] <= ai) {
                t.insert(nums[i]);
                i++;
            }

            if (i == 0)  ans[qIndx] = -1;
            else    ans[qIndx] = t.getMax(xi);
        }

        return ans;
    }
};
```

</details>
