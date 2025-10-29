<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name: Yuvaram S</h3>
<h3>Register Number: 212224230315</h3>
<H3>Aim:</H3>
<p>To ImplementA * Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>

``````
// A* Search Algorithm
1.  Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)

3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"

    b) pop q off the open list
  
    c) generate q's 8 successors and set their 
       parents to q
   
    d) for each successor
        i) if successor is the goal, stop search
        
        ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          
          successor.f = successor.g + successor.h

        iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor

        iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
     end (for loop)
  
    e) push q on the closed list
    end (while loop)

``````

<hr>

## PROGRAM:
```
from collections import defaultdict

H_dist = {}

def a_star(start_node, stop_node):
    open_set = {start_node}
    closed_set = set()
    g_cost = {start_node: 0}
    parent = {start_node: start_node}

    while open_set:
        current = min(open_set, key=lambda x: g_cost[x] + heuristic(x))

        if current == stop_node:
            return construct_path(parent, start_node, stop_node)

        open_set.remove(current)
        closed_set.add(current)

        for neighbor, weight in get_neighbors(current):
            tentative_g = g_cost[current] + weight

            if neighbor in closed_set:
                continue

            if neighbor not in open_set or tentative_g < g_cost.get(neighbor, float('inf')):
                parent[neighbor] = current
                g_cost[neighbor] = tentative_g
                open_set.add(neighbor)

    print("Path does not exist!")
    return None

def get_neighbors(node):
    return Graph_nodes.get(node, [])

def heuristic(node):
    return H_dist.get(node, 0)

def construct_path(parents, start, goal):
    path = [goal]
    while parents[goal] != goal:
        goal = parents[goal]
        path.append(goal)
    path.reverse()
    print("Path found:", path)
    return path

graph = defaultdict(list)
n, e = map(int, input().split())

for _ in range(e):
    u, v, cost = input().split()
    cost = int(cost)
    graph[u].append((v, cost))
    graph[v].append((u, cost))

for _ in range(n):
    node, h = input().split()
    H_dist[node] = int(h)

Graph_nodes = graph

start = input().strip()
goal = input().strip()

a_star(start, goal)

```
<h2>Sample Graph I</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/b1377c3f-011a-4c0f-a843-516842ae056a)

<hr>
<h2>Sample Input</h2>
<hr>
10 14 <br>
A B 6 <br>
A F 3 <br>
B D 2 <br>
B C 3 <br>
C D 1 <br>
C E 5 <br>
D E 8 <br>
E I 5 <br>
E J 5 <br>
F G 1 <br>
G I 3 <br>
I J 3 <br>
F H 7 <br>
I H 2 <br>
A 10 <br>
B 8 <br>
C 5 <br>
D 7 <br>
E 3 <br>
F 6 <br>
G 5 <br>
H 3 <br>
I 1 <br>
J 0 <br>
<hr>
<h2>Sample Output</h2>
<img width="1164" height="766" alt="image" src="https://github.com/user-attachments/assets/d5d4c220-3ab6-4d11-a738-c93098baab57" />

<hr>
Path found: ['A', 'F', 'G', 'I', 'J']


<hr>
<h2>Sample Graph II</h2>
<hr>


<hr>
<h2>Sample Input</h2>
<hr>
6 6 <br>
A B 2 <br>
B C 1 <br>
A E 3 <br>
B G 9 <br>
E D 6 <br>
D G 1 <br>
A 11 <br>
B 6 <br>
C 99 <br>
E 7 <br>
D 1 <br>
G 0 <br>
<hr>
<h2>Sample Output</h2>
<img width="1133" height="467" alt="image" src="https://github.com/user-attachments/assets/7f98f743-45ac-4b8b-a4c2-899c6e0f890f" />

<hr>
Path found: ['A', 'E', 'D', 'G']
