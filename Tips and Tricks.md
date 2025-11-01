

# *To Eliminate The TLE TRICKS:* 
# *Problem Concept: “Repeated membership checks in a list”*

```python 
result = []
for val in data:
    if val not in nums:   # O(n) each time!
        result.append(val)

```
*Let’s trace it 👇*

|`val`|Check `val not in nums`|Steps required|
|---|---|---|
|5|Python checks 3 → 5|2 steps|
|7|checks 3, 5, 9, 12, 20|5 steps|
|9|checks 3, 5, 9|3 steps|
|11|checks 3, 5, 9, 12, 20|5 steps|
|20|checks 3, 5, 9, 12, 20|5 steps|
|25|checks all elements|5 steps|
|30|checks all elements|5 steps|

*So total = **2 + 5 + 3 + 5 + 5 + 5 + 5 = 30 steps***  
*Even for small lists it’s already inefficient.*

## *⚡ The Better Way — Use a Set*

*If we convert `nums` into a `set`, Python uses **hashing** internally.*

*That makes lookups average **O(1)** time — no looping through elements.*

```python
nums = {3, 5, 9, 12, 20}   # or set([3, 5, 9, 12, 20])
result = []

for val in data:
    if val not in nums:   # O(1) average time
        result.append(val)

```

*Now, each check is almost instant, regardless of how many elements are in `nums`.*

*Even if you have 100,000 numbers, `x in set(nums)` is still very fast.*

## *🧩 Summary (for your notes)*

|Concept|Description|Example|Time|
|---|---|---|---|
|Membership testing (`x in list`)|Checks each element one by one|`5 in [1,2,3,4,5]` → True after 5 checks|O(n)|
|Membership testing (`x in set`)|Uses hashing; finds item directly|`5 in {1,2,3,4,5}` → True instantly|O(1)|
|When to use `set`|When you need to test membership many times|Filtering, duplicates, etc.|✅ Fast|
|When to use `list`|When you care about **order** or need to **index** items|`nums[2]` → 3|🚫 Slow for lookup|

---




