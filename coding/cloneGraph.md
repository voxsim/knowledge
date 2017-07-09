## Text
Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors.
OJ's undirected graph serialization: Nodes are labeled uniquely.
We use # as a separator for each node, and , as a separator for node label and each neighbor of the node.
As an example, consider the serialized graph {0,1,2#1,2#2,2}.
The graph has a total of three nodes, and therefore contains three parts as separated by #.
First node is labeled as 0. Connect node 0 to both nodes 1 and 2.
Second node is labeled as 1. Connect node 1 to node 2.
Third node is labeled as 2. Connect node 2 to node 2 (itself), thus forming a self-cycle.
Visually, the graph looks like the following:

```
    1
   / \
  /   \
 0 --- 2
      / \
      \_/
```

## Solution
```javascript
function cloneGraph(node) {
  let isAlreadyCloned = {};
  function _clone(node) {
    if(!!isAlreadyCloned[node.id]) {
      return isAlreadyCloned[node.id];
    }
    
    let newNode = {id: node.id, neighbours: []};
    isAlreadyCloned[node.id] = newNode;
    for(let i=0; i<node.neighbours.length; i++) {
      newNode.neighbours.push(_clone(node.neighbours[i]));
    }
    return newNode;
  }
  
  return _clone(node);
}
```

## Explaining

## Testcase
```javascript
let node0 = {id: 0, neighbours: []};
let node1 = {id: 1, neighbours: []};
let node2 = {id: 2, neighbours: [node0, node1]};
node2.neighbours.push(node2);
cloneGraph(node2);
```

## Complexity
O(n)
