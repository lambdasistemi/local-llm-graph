# Local LLM Ecosystem Graph

Interactive knowledge graph of the local LLM ecosystem — models, inference engines, quantization formats, API proxies, coding assistants, and hardware. Focused on AMD Strix Halo (128GB) and Claude Code hybrid cloud/local setups.

## What's in the graph

- **53 nodes** across 8 categories: models, engines, formats, proxies, assistants, hardware, hubs, protocols
- **80 edges** showing compatibility, translation, and dependency relationships
- **3 guided tutorials**: hardware setup, hybrid Claude Code routing, model selection

## Data format

Uses [graph-browser](https://github.com/lambdasistemi/graph-browser) JSON format. See `data/` directory.

## Updating

Edit `data/graph.json` to add nodes/edges. Validate with:

```bash
node -e "
  const d=require('./data/graph.json');
  const c=require('./data/config.json');
  const ids=new Set(d.nodes.map(n=>n.id));
  const kinds=Object.keys(c.kinds);
  let ok=true;
  d.nodes.forEach(n=>{
    if(!kinds.includes(n.kind)){console.error('Unknown kind: '+n.kind+' on node '+n.id);ok=false}
  });
  d.edges.forEach((e,i)=>{
    if(!ids.has(e.source)){console.error('Bad source e'+i+': '+e.source);ok=false}
    if(!ids.has(e.target)){console.error('Bad target e'+i+': '+e.target);ok=false}
  });
  if(ok) console.log(d.nodes.length+' nodes, '+d.edges.length+' edges — OK');
  else process.exit(1);
"
```
