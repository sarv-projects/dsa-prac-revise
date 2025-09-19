
# Table of Contents

## Section 1: Arrays & Hashing
- [Contains Duplicate [Must Do]](#1️⃣-contains-duplicate-must-do)
- [Valid Anagram](#2️⃣-valid-anagram)
- [Two Sum [Must Do]](#3️⃣-two-sum-must-do)
- [Group Anagrams [Must Do]](#4️⃣-group-anagrams-must-do)
- [Top K Frequent Elements [Must Do]](#5️⃣-top-k-frequent-elements-must-do)
- [Encode and Decode Strings](#6️⃣-encode-and-decode-strings)
- [Product of Array Except Self [Must Do]](#7️⃣-product-of-array-except-self-must-do)
- [Valid Sudoku [Must Do]](#8️⃣-valid-sudoku-must-do)
- [Longest Consecutive Sequence [Must Do]](#9️⃣-longest-consecutive-sequence-must-do)

## Section 2: Two Pointers
- [Valid Palindrome [Must Do]](#1️⃣-valid-palindrome-must-do)
- [Two Sum II – Input Array Is Sorted [Must Do]](#2️⃣-two-sum-ii--input-array-is-sorted-must-do)
- [3Sum [Must Do]](#3️⃣-3sum-must-do)
- [Container With Most Water [Must Do]](#4️⃣-container-with-most-water-must-do)
- [Trapping Rain Water [Must Do]](#5️⃣-trapping-rain-water-must-do)

## Section 3: Sliding Window
- [Best Time to Buy and Sell Stock [Must Do]](#1️⃣-best-time-to-buy-and-sell-stock-must-do)
- [Longest Substring Without Repeating Characters [Must Do]](#2️⃣-longest-substring-without-repeating-characters-must-do)
- [Longest Repeating Character Replacement [Must Do]](#3️⃣-longest-repeating-character-replacement-must-do)
- [Permutation in String [Must Do]](#4️⃣-permutation-in-string-must-do)
- [Minimum Window Substring [Must Do]](#5️⃣-minimum-window-substring-must-do)
- [Sliding Window Maximum [Must Do]](#6️⃣-sliding-window-maximum-must-do)





## Section 1: Arrays & Hashing

---

### 1️⃣ Contains Duplicate \[Must Do]

**Pattern / Idea:** Use a set to track seen elements. If a number repeats, return True.

**Pseudocode:**

* Initialize empty set `seen`
* For each number `n` in array:

  * If `n` in `seen`, return True
  * Else, add `n` to `seen`
* Return False

**Python Code:**

```python
def containsDuplicate(nums):
    seen = set()
    for n in nums:
        if n in seen:
            return True
        seen.add(n)
    return False
```

**T.C.:** O(n)

**S.C.:** O(n)

**Quick Recall Hack:** "Set = guard against repeats."

---

### 2️⃣ Valid Anagram

**Pattern / Idea:** Count characters in both strings and compare.

**Pseudocode:**

* If lengths differ → False
* Count characters in both strings
* Compare counts

**Python Code:**

```python
from collections import Counter
def isAnagram(s, t):
    return Counter(s) == Counter(t)
```

**T.C.:** O(n)

**S.C.:** O(n)

**Quick Recall Hack:** "Same letters, same count."

---

### 3️⃣ Two Sum \[Must Do]

**Pattern / Idea:** Use hash map to store numbers and look for complement.

**Pseudocode:**

* Initialize empty dictionary `d`
* For each index i, num in nums:

  * If target - num in d → return \[d\[target-num], i]
  * Else, store num in d with index

**Python Code:**

```python
def twoSum(nums, target):
    d = {}
    for i, num in enumerate(nums):
        if target - num in d:
            return [d[target - num], i]
        d[num] = i
```

**T.C.:** O(n)

**S.C.:** O(n)

**Quick Recall Hack:** "Store, check, return."

---

### 4️⃣ Group Anagrams \[Must Do]

**Pattern / Idea:** Strings with same sorted characters belong together. Use hash map.

**Pseudocode:**

* Initialize `groups = defaultdict(list)`
* For each string `s` in strs:

  * Key = sorted(s) → join back to string
  * Append s to `groups[key]`
* Return all groups

**Python Code:**

```python
from collections import defaultdict
def groupAnagrams(strs):
    groups = defaultdict(list)
    for s in strs:
        key = ''.join(sorted(s))
        groups[key].append(s)
    return list(groups.values())
```

**T.C.:** O(n k log k) → n = #strings, k = avg length

**S.C.:** O(n k)

**Quick Recall Hack:** "Sort letters → group."

---

### 5️⃣ Top K Frequent Elements \[Must Do]

**Pattern / Idea:** Count frequency → use heap or bucket sort.

**Pseudocode:**

* Count elements using Counter
* Sort elements by frequency
* Return top K

**Python Code:**

```python
from collections import Counter
def topKFrequent(nums, k):
    count = Counter(nums)
    return [item for item, freq in count.most_common(k)]
```

**T.C.:** O(n log k)

**S.C.:** O(n)

**Quick Recall Hack:** "Count → top K."

---

### 6️⃣ Encode and Decode Strings

**Pattern / Idea:** Encode using delimiter; decode by splitting.

**Pseudocode:**

* Encode: append length + '#' + string
* Decode: parse length, extract substring

**Python Code:**

```python
def encode(strs):
    return ''.join(f'{len(s)}#{s}' for s in strs)

def decode(s):
    res, i = [], 0
    while i < len(s):
        j = i
        while s[j] != '#':
            j += 1
        length = int(s[i:j])
        res.append(s[j+1:j+1+length])
        i = j + 1 + length
    return res
```

**T.C.:** O(n)

**S.C.:** O(n)

**Quick Recall Hack:** "Length#String → easy parse."

---

### 7️⃣ Product of Array Except Self \[Must Do]

**Pattern / Idea:** Prefix & suffix product arrays.

**Pseudocode:**

* Left product: accumulate from start
* Right product: accumulate from end
* Multiply left\[i] \* right\[i]

**Python Code:**

```python
def productExceptSelf(nums):
    n = len(nums)
    res = [1]*n
    prefix = 1
    for i in range(n):
        res[i] = prefix
        prefix *= nums[i]
    suffix = 1
    for i in range(n-1, -1, -1):
        res[i] *= suffix
        suffix *= nums[i]
    return res
```

**T.C.:** O(n)

**S.C.:** O(1) extra (res counts)

**Quick Recall Hack:** "Prefix \* Suffix = answer."

---

### 8️⃣ Valid Sudoku \[Must Do]

**Pattern / Idea:** Check rows, columns, and 3x3 blocks for duplicates.

**Pseudocode:**

* For each row, col, block:

  * Maintain set
  * If duplicate → False
* Else → True

**Python Code:**

```python
def isValidSudoku(board):
    rows = [set() for _ in range(9)]
    cols = [set() for _ in range(9)]
    boxes = [set() for _ in range(9)]
    for i in range(9):
        for j in range(9):
            num = board[i][j]
            if num == '.':
                continue
            if num in rows[i] or num in cols[j] or num in boxes[(i//3)*3 + j//3]:
                return False
            rows[i].add(num)
            cols[j].add(num)
            boxes[(i//3)*3 + j//3].add(num)
    return True
```

**T.C.:** O(1) → board fixed size

**S.C.:** O(1)

**Quick Recall Hack:** "Row+Col+Box sets."

---

### 9️⃣ Longest Consecutive Sequence \[Must Do]

**Pattern / Idea:** Use a set to expand sequences from sequence starts.

**Pseudocode:**

* Put nums in set
* For each num:

  * If num-1 not in set → start sequence
  * Count consecutive numbers
  * Track max length

**Python Code:**

```python
def longestConsecutive(nums):
    num_set = set(nums)
    max_len = 0
    for n in num_set:
        if n-1 not in num_set:
            length = 1
            while n+length in num_set:
                length += 1
            max_len = max(max_len, length)
    return max_len
```

**T.C.:** O(n)

**S.C.:** O(n)

**Quick Recall Hack:** "Sequence start → expand."


Perfect. Let’s tackle the **Two Pointers** section in your requested **Problem Format**, marking **must-do non-FAANG problems in brackets**.

---

## Section 2: Two Pointers

---

### 1️⃣ Valid Palindrome \[Must Do]

**Pattern / Idea:** Use two pointers from start and end; skip non-alphanumeric.

**Pseudocode:**

* i = 0, j = len(s)-1
* While i < j:

  * If s\[i] not alnum → i++
  * If s\[j] not alnum → j--
  * If s\[i].lower() != s\[j].lower() → return False
  * Else i++, j--
* Return True

**Python Code:**

```python
def isPalindrome(s):
    i, j = 0, len(s)-1
    while i < j:
        while i < j and not s[i].isalnum():
            i += 1
        while i < j and not s[j].isalnum():
            j -= 1
        if s[i].lower() != s[j].lower():
            return False
        i += 1
        j -= 1
    return True
```

**T.C.:** O(n)

**S.C.:** O(1)

**Quick Recall Hack:** "Skip junk → match ends."

---

### 2️⃣ Two Sum II – Input Array Is Sorted \[Must Do]

**Pattern / Idea:** Sorted array → two pointers from ends.

**Pseudocode:**

* i = 0, j = len(nums)-1
* While i < j:

  * sum = nums\[i] + nums\[j]
  * If sum == target → return \[i+1, j+1]
  * If sum < target → i++
  * Else → j--

**Python Code:**

```python
def twoSumSorted(nums, target):
    i, j = 0, len(nums)-1
    while i < j:
        s = nums[i] + nums[j]
        if s == target:
            return [i+1, j+1]
        elif s < target:
            i += 1
        else:
            j -= 1
```

**T.C.:** O(n)

**S.C.:** O(1)

**Quick Recall Hack:** "Sum too small → right up, too big → left down."

---

### 3️⃣ 3Sum \[Must Do]

**Pattern / Idea:** Sort array → fix one element → two pointers for remaining two.

**Pseudocode:**

* Sort nums
* For i in range(n):

  * Skip duplicates
  * left=i+1, right=n-1
  * While left < right:

    * total = nums\[i]+nums\[left]+nums\[right]
    * If total == 0 → add triplet, left++, right-- (skip duplicates)
    * If total < 0 → left++
    * Else → right--

**Python Code:**

```python
def threeSum(nums):
    nums.sort()
    res = []
    for i in range(len(nums)):
        if i > 0 and nums[i] == nums[i-1]:
            continue
        left, right = i+1, len(nums)-1
        while left < right:
            total = nums[i] + nums[left] + nums[right]
            if total == 0:
                res.append([nums[i], nums[left], nums[right]])
                left += 1
                right -= 1
                while left < right and nums[left] == nums[left-1]:
                    left += 1
                while left < right and nums[right] == nums[right+1]:
                    right -= 1
            elif total < 0:
                left += 1
            else:
                right -= 1
    return res
```

**T.C.:** O(n²)

**S.C.:** O(n)

**Quick Recall Hack:** "Sort + fix one + two pointers."

---

### 4️⃣ Container With Most Water \[Must Do]

**Pattern / Idea:** Two pointers → maximize area = min(height) \* width.

**Pseudocode:**

* left=0, right=n-1, max\_area=0
* While left < right:

  * area = min(height\[left], height\[right])\*(right-left)
  * Update max\_area
  * Move smaller height pointer

**Python Code:**

```python
def maxArea(height):
    left, right = 0, len(height)-1
    max_area = 0
    while left < right:
        max_area = max(max_area, min(height[left], height[right])*(right-left))
        if height[left] < height[right]:
            left += 1
        else:
            right -= 1
    return max_area
```

**T.C.:** O(n)

**S.C.:** O(1)

**Quick Recall Hack:** "Move smaller → potential increase."

---

### 5️⃣ Trapping Rain Water \[Must Do]

**Pattern / Idea:** Two pointers → track left\_max and right\_max → water = min(left\_max, right\_max)-height.

**Pseudocode:**

* left=0, right=n-1, left\_max=0, right\_max=0, water=0
* While left < right:

  * If height\[left] < height\[right]:

    * left\_max = max(left\_max, height\[left])
    * water += left\_max - height\[left]
    * left++
  * Else:

    * right\_max = max(right\_max, height\[right])
    * water += right\_max - height\[right]
    * right--

**Python Code:**

```python
def trap(height):
    left, right = 0, len(height)-1
    left_max = right_max = water = 0
    while left < right:
        if height[left] < height[right]:
            left_max = max(left_max, height[left])
            water += left_max - height[left]
            left += 1
        else:
            right_max = max(right_max, height[right])
            water += right_max - height[right]
            right -= 1
    return water
```

**T.C.:** O(n)

**S.C.:** O(1)

**Quick Recall Hack:** "Two sides → trap water."

---



---

## Section 3: Sliding Window

---

### 1️⃣ Best Time to Buy and Sell Stock \[Must Do]

**Pattern / Idea:** Track the minimum price so far. Maximum profit = current price - min price.

* You don’t need nested loops; just one pass.


**Pseudocode:**

* Initialize `min_price = inf`, `max_profit = 0`
* For each price in prices:

  * Update min\_price = min(min\_price, price)
  * Update max\_profit = max(max\_profit, price - min\_price)
* Return max\_profit

**Python Code:**

```python
def maxProfit(prices):
    min_price = float('inf')
    max_profit = 0
    for price in prices:
        min_price = min(min_price, price)
        max_profit = max(max_profit, price - min_price)
    return max_profit
```

**T.C.:** O(n)

**S.C.:** O(1)

**Quick Recall Hack:** "Track min, update profit."

---

### 2️⃣ Longest Substring Without Repeating Characters \[Must Do]

**Pattern / Idea:** Sliding window → expand window until repeat → shrink from left.

* Use set to check duplicates.


**Pseudocode:**

* left=0, max\_len=0, seen=set()
* For right in range(len(s)):

  * While s\[right] in seen:

    * Remove s\[left] from set
    * left +=1
  * Add s\[right] to set
  * Update max\_len = max(max\_len, right-left+1)

**Python Code:**

```python
def lengthOfLongestSubstring(s):
    seen = set()
    left = 0
    max_len = 0
    for right in range(len(s)):
        while s[right] in seen:
            seen.remove(s[left])
            left += 1
        seen.add(s[right])
        max_len = max(max_len, right-left+1)
    return max_len
```

**T.C.:** O(n)

**S.C.:** O(min(n, charset))

**Quick Recall Hack:** "Expand → shrink when repeat."

---

### 3️⃣ Longest Repeating Character Replacement \[Must Do]

**Pattern / Idea:** Sliding window → keep track of most frequent char in window.

* Max length window = window size - max\_freq ≤ k


**Pseudocode:**

* left=0, count={}
* max\_count=0, max\_len=0
* For right in range(len(s)):

  * count\[s\[right]] +=1
  * max\_count = max(max\_count, count\[s\[right]])
  * If window\_size - max\_count > k → remove s\[left], left++
  * Update max\_len

**Python Code:**

```python
def characterReplacement(s, k):
    count = {}
    left = max_count = max_len = 0
    for right in range(len(s)):
        count[s[right]] = count.get(s[right], 0) + 1
        max_count = max(max_count, count[s[right]])
        while (right - left + 1) - max_count > k:
            count[s[left]] -= 1
            left += 1
        max_len = max(max_len, right - left + 1)
    return max_len
```

**T.C.:** O(n)

**S.C.:** O(26) → English letters

**Quick Recall Hack:** "Window - max freq ≤ k → shrink."

---

### 4️⃣ Permutation in String \[Must Do]

**Pattern / Idea:** Check if a window in s2 is a permutation of s1.

* Fixed window size = len(s1), check counts match.


**Pseudocode:**

* Build freq of s1
* Slide window of size len(s1) over s2
* Keep freq of current window
* If matches → True

**Python Code:**

```python
from collections import Counter
def checkInclusion(s1, s2):
    len1 = len(s1)
    s1_count = Counter(s1)
    window_count = Counter()
    for i in range(len(s2)):
        window_count[s2[i]] += 1
        if i >= len1:
            if window_count[s2[i - len1]] == 1:
                del window_count[s2[i - len1]]
            else:
                window_count[s2[i - len1]] -= 1
        if window_count == s1_count:
            return True
    return False
```

**T.C.:** O(n)

**S.C.:** O(26) → letters

**Quick Recall Hack:** "Slide window, compare counts."

---

### 5️⃣ Minimum Window Substring \[Must Do]

**Pattern / Idea:** Sliding window → include all chars of t, shrink left as much as possible.

* Keep counts of t, compare with window counts.


**Pseudocode:**

* Build count\_t = Counter(t)
* left=0, formed=0, window\_counts={}
* Expand right: add s\[right] to window\_counts
* While window satisfies t:

  * update min\_len, min\_start
  * remove s\[left] from window\_counts, left++
* Return substring

**Python Code:**

```python
from collections import Counter
def minWindow(s, t):
    if not t or not s:
        return ""
    count_t = Counter(t)
    window_counts = {}
    have = 0
    need = len(count_t)
    res = [float("inf"), 0, 0]  # length, start, end
    left = 0
    for right, char in enumerate(s):
        window_counts[char] = window_counts.get(char, 0) + 1
        if char in count_t and window_counts[char] == count_t[char]:
            have += 1
        while have == need:
            if right - left + 1 < res[0]:
                res = [right - left + 1, left, right]
            window_counts[s[left]] -= 1
            if s[left] in count_t and window_counts[s[left]] < count_t[s[left]]:
                have -= 1
            left += 1
    l = res[1]
    r = res[2]
    return s[l:r+1] if res[0] != float("inf") else ""
```

**T.C.:** O(n + m) → n=len(s), m=len(t)

**S.C.:** O(26) → letters

**Quick Recall Hack:** "Expand to satisfy, shrink to minimize."

---

### 6️⃣ Sliding Window Maximum \[Must Do]

**Pattern / Idea:** Use deque to maintain decreasing elements → max at deque\[0].

* Remove smaller elements from back.


**Pseudocode:**

* Initialize deque
* For i in range(len(nums)):

  * Remove indices out of window
  * Remove indices whose nums < nums\[i] from back
  * Append i
  * If i >= k-1 → res.append(nums\[deque\[0]])

**Python Code:**

```python
from collections import deque
def maxSlidingWindow(nums, k):
    dq = deque()
    res = []
    for i, n in enumerate(nums):
        while dq and dq[0] <= i - k:
            dq.popleft()
        while dq and nums[dq[-1]] < n:
            dq.pop()
        dq.append(i)
        if i >= k - 1:
            res.append(nums[dq[0]])
    return res
```

**T.C.:** O(n)

**S.C.:** O(k)

**Quick Recall Hack:** "Deque keeps max at front."

---





