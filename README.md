# FamilyTreeWithText



<!DOCTYPE html>
<meta charset="utf-8">
<head>
  <title>Tree layout</title>
</head>

<style>
.node {
  fill: steelblue;
  stroke: none;
}

.link {
  fill: blue;
  stroke: #ccc;
  stroke-width: 1px;
}
</style>

<body>
  <br>
  <svg width="500" height="500" fill="blue">
    <g transform="translate(5, 20)">
      <g class="links"></g>
      <g class="nodes"></g>
    </g>
  </svg>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/d3/4.2.2/d3.min.js"></script>
  <script>
var data = {
  "name": "A1",
  "children": [
    {
      "name": "B1",
      "children": [
        {
          "name": "C1",
          "value": 100
        },
        {
          "name": "C2",
          "value": 300
        },
        {
          "name": "C3",
          "value": 200
        }
      ]
    },
    {
      "name": "B2",
      "value": 200
    },
    {
      "name": "B2",
      "value": 200
    },
    {
      "name": "B2",
      "value": 200
    },
    {
      "name": "B2",
      "value": 200
    },
    {
      "name": "B2",
      "value": 200
    }
  ]
}

var treeLayout = d3.tree()
  .size([400, 200])

var root = d3.hierarchy(data)

treeLayout(root)

// Nodes
const svg = d3.select('svg g.nodes')
  .selectAll('circle.node')
  .data(root.descendants())
  .enter()
  .append('circle')
  .classed('node', true)
  .attr('cx', function(d) {return d.x;})
  .attr('cy', function(d) {return d.y;})
  .attr('r', 6);

// Links
d3.select('svg g.links')
  .selectAll('path.link')
  .data(root.links())
  .enter()
  .append('path')
  .classed('link', true)
  .attr('d', function(d) {
    
    
    return "M"+`${d.source.x} ${d.source.y} C ${d.source.x} ${(d.source.y+d.target.y)/2}
     ${(d.source.x+d.target.x)/2} ${(d.source.y+d.target.y)/2}  ${d.target.x} ${d.target.y} Z`;})
  

     const text = svg.append('g');
text.
select('text').
data(root.descendants())
.enter()
.append('text')
.attr('x',d=>d.x).attr('y',d=>d.y-2)
.text(d=>d.data.name);



var nodeEnter = d3.select('svg g .nodes').data(root.descendants())

	  .on("click",(d)=>console.log(d))


  </script>
</body>
</html>
