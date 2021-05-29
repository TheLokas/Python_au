# Algorithms

+ [House Robber II](#house-robber-ii)
+ [Design Twitter](#design-twitter)
+ [Min Stack](#min-stack)
+ [Implement Queue using Stacks](#implement-queue-using-stacks)
+ [House Robber](#house-robber)
+ [Merge K Sorted Lists](#merge-k-sorted-lists)
+ [K Closest Points to Origin](#k-closest-points-to-origin)
+ [Maximum Depth of N-ary Tree](#maximum-depth-of-n-ary-tree)
+ [Shortest Path In Binary Matrix](#shortest-path-in-binary-matrix)
+ [Is Graph Bipartite](#is-graph-bipartite)
+ [Cheapest Flights Within k Stops](#cheapest-flights-within-k-stops)
+ [Course Schedule II](#course-schedule-ii)
+ [Course Schedule](#course-schedule)
+ [Number of Islands](#number-of-islands)
+ [Implement Stack using Queues](#implement-stack-using-queues)


## House Robber II

https://leetcode.com/problems/house-robber-ii/

```python
def rob(self, nums: List[int]) -> int:
    if not nums: 
        return 0
    if len(nums)==1: return nums[0]
        
    def f(nums):
        prev_max = 0
        cur_max = 0
        for p in nums:
            temp = cur_max
            cur_max = max(cur_max, prev_max+p)
            prev_max = temp
        return cur_max  
    return max( f(nums[:-1]), f(nums[1:]))
```


## Design Twitter

https://leetcode.com/problems/design-twitter/

```python
def __init__(self):
    self.stack = list()
    self.fo = defaultdict(list)
def postTweet(self, userId: int, tweetId: int) -> None:
    self.stack.append([userId,tweetId]) 
def getNewsFeed(self, userId: int) -> List[int]:
    temp = list()
    for i in range(len(self.stack)-1,-1,-1):
        if self.stack[i][0] == userId or self.stack[i][0] in self.fo[userId]:
            temp.append(self.stack[i][1])
            if len(temp) == 10:
                break
    return temp 
        
def follow(self, followerId: int, followeeId: int) -> None:
    self.fo[followerId].append(followeeId)
def unfollow(self, followerId: int, followeeId: int) -> None:
    if followeeId in self.fo[followerId]:
        self.fo[followerId].remove(followeeId)
```


## Min Stack

https://leetcode.com/problems/min-stack/

```python
class MinStack:
    def __init__(self):
        self.stack = []
    def push(self, val: int) -> None:
        if self.stack:
            if val <= self.stack[-1][1]:
                self.stack.append((val,val))
            else:
                self.stack.append((val,(self.stack[-1][1])))
        else:
            self.stack.append((val,val))
        
    def pop(self) -> None:
        self.stack.pop()
    def top(self) -> int:
        return self.stack[-1][0]
    def getMin(self) -> int:
        return self.stack[-1][1]
```


## Implement Queue using Stacks

https://leetcode.com/problems/implement-queue-using-stacks/

```python
def __init__(self):
    self.queue = []
        
 def push(self, x: int) -> None:
    self.queue.append(x)
def pop(self) -> int:
    if len(self.queue) < 1:
        return None
    return self.queue.pop(0) 
def peek(self) -> int:
    if len(self.queue) < 1:
        return None
    return self.queue[0] 
def empty(self) -> bool:
    if len(self.queue) == 0:
        return True
    return False
```


## House Robber

https://leetcode.com/problems/house-robber/ 

```python
def rob(self, nums: List[int]) -> int:
    profits = [0]
    for i in range(len(nums)):
        if i == 0:
            profits.append(nums[i])  
        else:
            p = max(profits[i], profits[i-1] + nums[i])
            profits.append(p) 
    return profits[-1]    
```


## Merge K Sorted Lists

https://leetcode.com/problems/merge-k-sorted-lists/

```python
def mergeKLists(self, lists: List[ListNode]) -> ListNode:
    if not lists:
        return None
    if len(lists) == 1:
        return lists[0]
    mid = len(lists) // 2
    l = self.mergeKLists(lists[:mid]), 
    r = self.mergeKLists(lists[mid:])
    return self.merge(l, r)
    
def merge(self, l, r):
    prev = head = ListNode()
    while l and r:
        if l.val < r.val:
            head.next = l
            l = l.next
        else:
            head.next = r
            r = r.next
        head = head.next
    head.next = l or r
    return prev.next
```


## K Closest Points to Origin

https://leetcode.com/problems/k-closest-points-to-origin/

```python
def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
    points.sort(key=lambda x: pow((x[0]**2 + x[1]**2), 0.5))
    return points[:k]
```


## Maximum Depth of N-ary Tree

https://leetcode.com/problems/maximum-depth-of-n-ary-tree/

```python
def maxDepth(self, root: 'Node') -> int:
    queue = []
    if root: queue.append((root,1))
    depth = 0
    for (node, level) in queue:
        depth = level
        queue += [(child, level+1) for child in node.children]
    return depth
```


## Shortest Path In Binary Matrix 

https://leetcode.com/problems/shortest-path-in-binary-matrix/

```python
from collections import deque
class Solution:
    def shortestPathBinaryMatrix(self, grid: List[List[int]]) -> int:
        if grid[0][0] != 0:
            return -1
        n = len(grid)
        if n == 1:
            if grid[0][0] == 0:
                return 1
        dq = deque()
        dq.append([0, 0])
        length = 1
        while dq:
            length += 1
            for _ in range(len(dq)):
                x, y = dq.popleft()
                for i in [-1, 0, 1]:
                    for j in [-1, 0, 1]:
                        if i == 0 and j == 0:
                            continue
                        if 0 <= x + i < n and 0 <= y + j < n and grid[x + i][y + j] == 0:
                            if x + i == n - 1 and y + j == n - 1:
                                return length
                            dq.append([x + i, y + j])
                            grid[x + i][y + j] = 1
        return -1
```


## Is Graph Bipartite 

https://leetcode.com/problems/is-graph-bipartite/

```python
def isBipartite(self, graph):
    blank = 0
    red = 1
    green = 2
    n = len(graph)
    visited = [blank]*n
    print(visited)
    for i in range(n):
        if not visited[i]:
            que = deque([i])
            visited[i] = red
            while que:
                i = que.popleft()
                for j in graph[i]:
                    if visited[i] == visited[j]:
                        return False
                    if not visited[j]:
                        visited[j] = 3 - visited[i]
                        que.append(j)
    return True
```


## Cheapest Flights Within k Stops 

https://leetcode.com/problems/cheapest-flights-within-k-stops/

```python
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, K: int) -> int:
        flight_list = defaultdict(list)
        for s,d,c in flights:
            flight_list[s].append([c,d])
        search_list = [(0,src,0)]
        while(search_list):
            distance, curr, stops = heapq.heappop(search_list) 
            if curr == dst:
                return distance
            elif stops > K:
                continue
            for cost, des in flight_list[curr]: 
                heapq.heappush(search_list, (distance+cost,des, stops+1))
        return -1
```


## Course Schedule II

https://leetcode.com/problems/course-schedule-ii/

```python
from collections import deque
def dfs(self, curr, visited, adj_list, answer):
    visited[curr] = 1 
    for neighbor in adj_list[curr]:
        if neighbor not in visited:
            if self.dfs(neighbor, visited, adj_list, answer):
                return True
        elif visited[neighbor] == 1:
            return True
    visited[curr] = 2
    answer.appendleft(curr)
    return False
    
def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
    adj_list = [[] for i in range(numCourses)]
    for course, pre in prerequisites:
        adj_list[pre].append(course)
    visited = {}
    answer = deque()
    for curr in range(numCourses):
        if curr not in visited:
            if self.dfs(curr, visited, adj_list, answer):
                return []
    return answer
```


## Course Schedule

https://leetcode.com/problems/course-schedule/

```python
def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
    count = 0
    todo = {i: set() for i in range(numCourses)}
    outdegree = [[] for _ in range(numCourses)]
    for i in prerequisites:
        todo[i[0]].add(i[1])
        outdegree[i[1]].append(i[0])
    start = [i for i in range(numCourses) if not todo[i]]
    while start:
        newStart = []
        for i in start:
            count += 1
            for j in outdegree[i]:
                todo[j].remove(i)
                if not todo[j]:
                    newStart.append(j)
        start = newStart
    return count == numCourses
```


## Number of Islands

https://leetcode.com/problems/number-of-islands/

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        row, col = len(grid), len(grid[0])
        queue = deque([])
        count = 0
        for x in range(row):
            for y in range(col):
                if grid[x][y] == "1":
                    count+=1
                    queue.append((x,y))
                    self.bfs(grid, row, col, queue)
        return count
    def bfs(self, grid, row, col, queue):
        visited = set()
        while queue:
            x,y = queue.popleft()
            grid[x][y] = "visited"
            if (x,y) in visited: continue
            visited.add((x,y))
            for nx,ny in [[x+1,y],[x-1,y],[x,y+1],[x,y-1]]:
                if 0<=nx<row and 0<=ny<col and grid[nx][ny] == "1":
                    queue.append((nx,ny))
```


## Implement Stack using Queues

https://leetcode.com/problems/implement-stack-using-queues/

```python
def __init__(self):
    """
    Initialize your data structure here.
    """
    self.q1 = deque()
    self.q2 = deque()
    self._top = None
def push(self, x: int) -> None:
    """
    Push element x onto stack.
    """
    self.q1.append(x)
    self._top = x
def pop(self) -> int:
    """
    Removes the element on top of the stack and returns that element.
    """
    while len(self.q1) > 1:
        self._top = self.q1.popleft()
        self.q2.append(self._top)
    temp = self.q1.popleft()
    self.q1, self.q2 = self.q2, self.q1
    return temp
def top(self) -> int:
    """
    Get the top element.
    """
    return self._top
def empty(self) -> bool:
    """
    Returns whether the stack is empty.
    """
    return len(self.q1) == 0
```