<script>
  import * as d3 from "d3";

  /**
   * @typedef Datum
   * @type {{id: any, parentId: any, step: 0 | 1}}
   */
  /** @type {Datum[]} */
  export let data = [];

  /** @type {SVGGraphicsElement | undefined} */
  let ref;

  /** @type {import("d3").StratifyOperator<Datum>} */
  const stratify = d3.stratify();
  /** @type {import("d3").TreeLayout<Datum>} */
  const tree = d3.tree().nodeSize([16, 32]);
  const link = d3
    .link(d3.curveBumpY)
    .x((d) => d.x)
    .y((d) => d.y);

  $: root = tree(stratify(data));
  $: {
    if (ref) {
      const { x, y, width, height } = ref.getBBox();
      ref.setAttribute("width", width + "px");
      ref.setAttribute("height", height + "px");
      ref.setAttribute("viewBox", `${x} ${y} ${width} ${height}`);
    }
  }
</script>

<div class="StepPlot">
  <svg bind:this={ref}>
    <g fill="none" stroke="#555" stroke-opacity="0.4" stroke-width="1.5">
      {#each root.links() as d (`${d.source.id}-${d.target.id}`)}
        <path d={link(d)} />
      {/each}
    </g>
    <g fill="#999">
      {#each root.descendants() as d (d.id)}
        <circle cx={d.x} cy={d.y} r={3} data-step={d.data.step} />
      {/each}
    </g>
  </svg>
</div>
