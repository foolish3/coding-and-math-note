Minimum time required to produce m items (GFG) same task type
Consider n machines which produce same type of items but at different rate i.e., machine 1 takes a1 sec to produce an item, machine 2 takes a2 sec to produce an item. Given an array that contains the time required by ith machine to produce an item. Considering all machines are working simultaneously, the task is to find the minimum time required to produce m items.
Examples: 
Input : arr[] = {1, 2, 3}, m = 11
Output : 6
In 6 sec, machine 1 produces 6 items, machine 2 produces 3 items, and machine 3 produces 2 items. So to produce 11 items minimum 6 sec are required.
Input : arr[] = {5, 6}, m = 11
Output : 30
Answer: 
import math as mt
# Return the minimum time required to
# produce m items with given machines.
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
# Driver Code
arr = [1, 2, 3]
n = len(arr)
m = 11
print(minTime(arr, n, m) )





Q2 You are planning production for an order. You have a number of machines that each have a fixed number of days to produce an item. Given that all the machines operate simultaneously, determine the minimum number of days to produce the required order. (HR)
For example, you have to produce  items. You have three machines that take  days to produce an item. The following is a schedule of items produced:
Day Production  Count
2   2               2
3   1               3
4   2               5
6   3               8
8   2              10
It takes  days to produce  items using these machines.
Function Description
Complete the minimumTime function in the editor below. It should return an integer representing the minimum number of days required to complete the order.
minimumTime has the following parameter(s):
machines: an array of integers representing days to produce one item per machine
goal: an integer, the number of items required to complete the order
Input Format
The first line consist of two integers  and , the size of  and the target production.
The next line contains  space-separated integers, .
Constraints
Output Format
Return the minimum time required to produce  items considering all machines work simultaneously.
Sample Input 0
2 5
2 3
Sample Output 0
6
Explanation 0
In  days  can produce  items and  can produce  items. This totals up to .
Sample Input 1
3 10
1 3 4
Sample Output 1
7
Explanation 1
In  minutes,  can produce  items,  can produce  items and  can produce  item, which totals up to .

Efficient version
def minTime(machines, goal): 
    # make a modest guess of what the days may be, and use it as a starting point
    efficiency = [1.0/x for x in machines]
    lower_bound = int(goal / sum(efficiency)) - 1
    upper_bound = lower_bound + max(machines) + 1    
    while lower_bound < upper_bound -1:
        days = (lower_bound + upper_bound)//2
        produce = sum([days//x for x in machines])
        if produce >= goal:
            upper_bound = days
        elif produce < goal:
            lower_bound = days       
return upper_bound

minTime([2,3,2],10)


Q3 There are n cores of processor. Each core can process a task at a time. Different cores can process different tasks simultaneously without affecting others. Suppose, there are m tasks in queue and the processor has to process these m tasks. Again, these m tasks are not all of similar type. The type of task is denoted by a number. So, m tasks are represented as m consecutive numbers, same number represents same type of task, like 1 represents task of type 1, 2 for type 2 task and so on. (GFG) different task type, starting time

Initially, all the cores are free. It takes one unit of cost to start a type of task in a core, which is currently not running in that core. One unit cost will be charged at the starting to start tasks on each core. As an example, a core is running type 3 task and if we assign type 3 task again in that core, then cost for this assignment will be zero. But, if we assign type 2 task then cost for this assignment will be one unit. A core keeps processing a task until next task is assigned to that core.
Input : n = 3, m = 6, arr = {1, 2, 1, 3, 4, 1}
Output : 4

Input : n = 2, m = 6, arr = {1, 2, 1, 3, 2, 1}
Output : 4
Explanation : 

Input : n = 3, m = 31, 
arr = {7, 11, 17, 10, 7, 10, 2, 9, 2, 18, 8, 10, 20, 10, 3, 20,
       17, 17, 17, 1, 15, 10, 8, 3, 3, 18, 13, 2, 10, 10, 11}
Output : 18

Answer

# Function to find out the farthest
# position where one of the currently
# ongoing tasks will rehappen.
def find(arr, pos, m, isRunning):
 
    # Iterate form last to current
    # position and find where the
    # task will happen next.
    d = [0] * (m + 1)
    for i in range(m - 1, pos, -1):
     
        if isRunning[arr[i]]:
            d[arr[i]] = i
     
    # Find out maximum of all these positions
    # and it is the farthest position.
    maxipos = 0
    for ele in d:
        maxipos = max(ele, maxipos)
 
    return maxipos
 
# Function to find out minimum
# cost to process all the tasks
def mincost(n, m, arr):
 
    # freqarr[i][j] denotes the frequency
    # of type j task after position i
    # like in array 1, 2, 1, 3, 2, 1
    # frequency of type 1 task after
    # position 0 is 2. So, for this
    # array freqarr[0][1] = 2. Here,
    # i can range in between 0 to m-1 and
    # j can range in between 0 to m(though
    # there is not any type 0 task).
    freqarr = [[] for i in range(m)]
 
    # Fill up the freqarr vector from
    # last to first. After m-1 th position
    # frequency of all type of tasks will be
    # 0. Then at m-2 th position only frequency
    # of arr[m-1] type task will be increased
    # by 1. Again, in m-3 th position only
    # frequency of type arr[m-2] task will
    # be increased by 1 and so on.
    newvec = [0] * (m + 1)
    freqarr[m - 1] = newvec[:]
    for i in range(m - 2, -1, -1):
     
        nv = freqarr[i + 1][:]
        nv[arr[i + 1]] += 1
        freqarr[i] = nv[:]
     
    # isRunning[i] denotes whether type i
    # task is currently running in one
    # of the cores.
    # At the beginning no tasks are
    # running so all values are false.
    isRunning = [False] * (m + 1)
 
    # cost denotes total cost to assign tasks
    cost = 0
 
    # truecount denotes number of occupied cores
    truecount = 0
 
    # iterate through each task
    # and find the total cost.
    for i in range(0, m):
 
        # ele denotes type of task.
        ele = arr[i]
 
        # Case 1: if smae type of task is
        # currently running cost for this is 0.
        if isRunning[ele] == True:
            continue
 
        # Case 2: same type of task
        # is not currently running.
        else:
 
            # Subcase 1: if there is at least
            # one free core then assign this task
            # to that core at a cost of 1 unit.
            if truecount < n:
                cost += 1
                truecount += 1
                isRunning[ele] = True
             
            # Subcase 2: No core is free
            else:
 
                # here we will first find the minimum
                # frequency among all the ongoing tasks
                # in future.
                # If the minimum frequency is 0 then
                # there is at least one ongoing task
                # which will not occur again. Then we just
                # stop tha task.
                # If minimum frequency is >0 then, all the
                # tasks will occur at least once in future.
                # we have to find out which of these will
                # rehappen last among the all ongoing tasks.
 
                # set minimum frequency to a big number
                mini = 100000
 
                # set index of minimum frequency task to 0.
                miniind = 0
 
                # find the minimum frequency task
                # type(miniind) and frequency(mini).
                for j in range(1, m + 1):
                    if isRunning[j] and mini > freqarr[i][j]:
                        mini = freqarr[i][j]
                        miniind = j
 
                # If minimum frequency is zero then just stop
                # the task and start the present task in that
                # core. Cost for this is 1 unit.
                if mini == 0:
                    isRunning[miniind] = False
                    isRunning[ele] = True
                    cost += 1
                 
                # If minimum frequency is nonzero then find
                # the farthest position where one of the
                # ongoing task will rehappen.
                # Stop that task and start present task
                # in that core.
                else:
 
                    # find out the farthest position
                    # using find function
                    farpos = find(arr, i, m, isRunning)
                    isRunning[arr[farpos]] = False
                    isRunning[ele] = True
                    cost += 1
                 
    # return total cost
    return cost
 
# Driver Code
if __name__ == "__main__":
 
    # Test case 1
    n1, m1 = 3, 6
    arr1 = [1, 2, 1, 3, 4, 1]
    print(mincost(n1, m1, arr1))
 
    # Test case 2
    n2, m2 = 2, 6
    arr2 = [1, 2, 1, 3, 2, 1]
    print(mincost(n2, m2, arr2))
 
    # Test case 3
    n3, m3 = 3, 31
    arr3 = [7, 11, 17, 10, 7, 10, 2, 9,
            2, 18, 8, 10, 20, 10, 3, 20,
            17, 17, 17, 1, 15, 10, 8, 3,
            3, 18, 13, 2, 10, 10, 11]
             
    print(mincost(n3, m3, arr3))


Q4 621. Task Scheduler (LC)
Share
Given a characters array tasks, representing the tasks a CPU needs to do, where each letter represents a different task. Tasks could be done in any order. Each task is done in one unit of time. For each unit of time, the CPU could complete either one task or just be idle.
However, there is a non-negative integer n that represents the cooldown period between two same tasks (the same letter in the array), that is that there must be at least n units of time between any two same tasks. Different task type, cooldown time
Return the least number of units of times that the CPU will take to finish all the given tasks.
import collections
class Solution(object):
    def leastInterval(self, tasks, n):
        """
        :type tasks: List[str]
        :type n: int
        :rtype: int
        """
        count = collections.defaultdict(int)
        max_count = 0
        for task in tasks:
            count[task] += 1
            max_count = max(max_count, count[task])

        result = (max_count-1) * (n+1)
        for count in count.values():
            if count == max_count:
                result += 1
        return max(result, len(tasks))
