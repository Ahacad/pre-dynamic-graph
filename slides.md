---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: 'text-center'
highlighter: shiki
# show line numbers in code blocks
lineNumbers: true
# persist drawings in exports and build
drawings:
  persist: false
---

# Efficient Parallel Algorithms for Betweenness- and Closeness-Centrality in Dynamic Graphs

---

<div class="mt-36"></div>

- <span class="black">Introduction</span>
- <span class="text-gray-400">Properties on the graph</span>
- <span class="text-gray-400">Betweenness-centrality</span>
- <span class="text-gray-400">Closeness-centrality</span>
- <span class="text-gray-400">Conclusions</span>

---

Efficient <span class="text-red-600">Parallel Algorithms</span> for <span class="text-red-600">Betweenness- and Closeness-Centrality</span> in <span class="text-red-600">Dynamic Graphs</span>

<div class="mt-16"></div>

Some keywords

- Dynamic graph (how to calculate something on a dynamic graph)
- Parallel algorithm
- Betweenness- and closeness- centrality

---

# Dynamic graph

<div class='mt-16' />
<div class="flex">
<img width="200" src="/pics/1.png" />
<img width="200" src="/pics/2.png" />
<img width="200" src="/pics/3.png" />
<img width="200" src="/pics/4.png" />
</div>
<div class="flex">
<img width="200" src="/pics/5.png" />
<img width="200" src="/pics/6.png" />
<img width="200" src="/pics/7.png" />
<img width="200" src="/pics/8.png" />
</div>

---

# Parallel algorithm

- How to be parallel on a graph?

<div class="mt-10"/>

<div class="flex">
<img width="300" src="/pics/graph-plain.png" />

<img v-click at="1" class="ml-50" width="300" src="/pics/graph-plain2.png" />
</div>

<arrow v-click at="2" x1="400" y1="270" x2="550" y2="270" color="#b99095" width="2" arrowSize="1" />

<div v-click at="3" class="mt-10">

- <span class="text-red-600">BCC: biconnected components</span>(will cover this very soon)

</div>

---

# Closeness-centrality

<div class="mt-10"/>

$$
cc(v) = \frac{N - 1}{\sum_u dis(u, v)}
$$

<div class="mt-10"/>

<div class="flex justify-center"><img class="" width="300" src="/pics/cc.png" /> </div>

- $dis(u, v)$: shortest path length between $u$ and $v$
- how close you are to others


---

# Betweenness-centrality

<div class="mt-10"/>

$$
bc(v) = \sum_{s \neq v \neq t} \frac{\delta_{st}(v)}{\delta_{st}}
$$

- ratio of: shortest paths that pass through $v$ to shortest paths number
- measures the node's influence

<div class="mt-6"/>
<div class="flex justify-center"><img class="" width="300" src="/pics/bc.png" /> </div>

- <span class="text-blue-600">note that both the two centralites relate to *shortest path*</span>

---

# Dependency

<div class="mt-20"/>

Dependency of a vertex $s$ on another vertex $v$ on a graph $G$ is defined as:

$$
\delta_s[v] = \sum_{t \in G} \delta_{st}(v)
$$

- all the short paths that has to pass through v


---

# TOC

<div class="mt-22"></div>

- <span class="text-gray-400">Background</span>
- <span class="text-black">Properties on the graph</span>
- <span class="text-gray-400">Betweenness-centrality</span>
- <span class="text-gray-400">Closeness-centrality</span>
- <span class="text-gray-400">Conclusions</span>

---

# Techniques mentioned

<div class="mt-10"/>

- Batch update
- BCC (Biconnected component decomposition)
- 
- Redundant nodes

---

# Batch update


---

# BCC

<div class="mt-10"/>

- maximal *biconnected subgrarph*
  - the graph remain connected even if remove any node

<img class="ml-50" width="300" src="/pics/bcc.png" />

<div class="mt-6"/>

- <span class="text-teal-600">BCC help limit the scope of BFS when calculating centralities</span><sup>3,4</sup>

---

# Redundant nodes
<div class="mt-10"/>

<img width="150" src="/pics/r3r4.png" />

<arrow x1="260" y1="240" x2="200" y2="220" color="#b99095" width="2" arrowSize="1" />

<arrow x1="220" y1="340" x2="160" y2="280" color="#b99095" width="2" arrowSize="1" />

<div class="mt-8"/>

- $R_3$: three neighbors of $v$ are connected to each other
- $R_4$: four neighbors of $v$ are connected to each other
- shortest path does not pass through $v$
- <span class="text-teal-700">we can possibly save computation</span>
- the changes are recorded, so no need to scan the whole graph every time


---

# TOC

<div class="mt-22"></div>

- <span class="text-gray-400">Background</span>
- <span class="text-gray-400">Properties on the graph</span>
- <span class="text-black">Betweenness-centrality</span>
- <span class="text-gray-400">Closeness-centrality</span>
- <span class="text-gray-400">Conclusions</span>

---

# Betweenness centrality

---

## Algorithm

---

# Implementation

---

# Results


<div class="mt-10"/>
<div class="flex justify-center"><img class="" width="500" src="/pics/bc-result.png" /> </div>

- the reuslts are very good

---

# TOC

<div class="mt-22"></div>

- <span class="text-gray-400">Background</span>
- <span class="text-gray-400">Properties on the graph</span>
- <span class="text-gray-400">Betweenness-centrality</span>
- <span class="text-black">Closeness-centrality</span>
- <span class="text-gray-400">Conclusions</span>

---

# Closeness centrality

---

# TOC

<div class="mt-22"></div>

- <span class="text-gray-400">Background</span>
- <span class="text-gray-400">Properties on the graph</span>
- <span class="text-gray-400">Betweenness-centrality</span>
- <span class="text-gray-400">Closeness-centrality</span>
- <span class="text-black">Conclusions</span>

---

# Conclusions

<div class="mt-10"></div>

What learned:

- Several centrality measurements <sup>[2]</sup>
- Ideas on calculating some properties on graph, especially in parallel

Upsides:
- Clear theoretical derivations

Downsides:
- The algorithm now only works on unweighted and undirected graphs (mentioned in future works)
- use previous people's works, really a lot (you need to read at least another 3 papers to understand the author's work)
  - some modifications on previous works to improve efficiency



---

# References

- [1] F. Jamour, S. Skiadopoulos, and P. Kalnis, “Parallel Algorithm for Incremental Betweenness Centrality on Large Graphs,” IEEE Trans. Parallel Distrib. Syst., vol. 29, no. 3, pp. 659–672, Mar. 2018, doi: 10.1109/TPDS.2017.2763951.



---
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
---

# Code

Use code snippets and get the highlighting directly![^1]

```ts {all|2|1-6|9|all}
interface User {
  id: number
  firstName: string
  lastName: string
  role: string
}

function updateUser(id: number, update: User) {
  const user = getUser(id)
  const newUser = {...user, ...update}  
  saveUser(id, newUser)
}
```

<arrow v-click="3" x1="400" y1="420" x2="230" y2="330" color="#564" width="3" arrowSize="1" />

[^1]: [Learn More](https://sli.dev/guide/syntax.html#line-highlighting)

<style>
.footnotes-sep {
  @apply mt-20 opacity-10;
}
.footnotes {
  @apply text-sm opacity-75;
}
.footnote-backref {
  display: none;
}
</style>
