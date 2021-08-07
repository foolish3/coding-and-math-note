# Minimum time required to produce m items (GFG) same task type
Consider n machines which produce same type of items but at different rate i.e., machine 1 takes a1 sec to produce an item, machine 2 takes a2 sec to produce an item. Given an array that contains the time required by ith machine to produce an item. Considering all machines are working simultaneously, the task is to find the minimum time required to produce m items
"""
Examples: 
Input : arr[] = {1, 2, 3}, m = 11
Output : 6
In 6 sec, machine 1 produces 6 items, machine 2 produces 3 items, and machine 3 produces 2 items. So to produce 11 items minimum 6 sec are required.
Input : arr[] = {5, 6}, m = 11
Output : 30
"""
Answer: 
import math as mt
def minTime(arr, n, m):
    # Initialise time, items equal to 0.
    t = 0
    while (1):
        items = 0
        # Calculating items at each second
        for i in range(n):
            items += (t // arr[i])
        # If items equal to m return time.
        if (items >= m):
            return t
        t += 1 # Increment time
arr = [1, 2, 3]
n = len(arr)
m = 11
print(minTime(arr, n, m))



