<template>
  <div class="vis-board" :id="vid">
  </div>
</template>
<script>
import * as d3 from 'd3'

export default {
  props: {
    vid: {
      type: String,
      required: true
    },
    model: {
      type: Object,
      default() {
        return  {
          Agents: []
        }
      }
    }
  },
  watch: {
    model: {
      deep: true,
      handler() {
        this.update();
      }
    }
  },
  data() {
    return {
      svg: null,
      width: null,
      height: null,
      x: null,
      y: null,
      particles: null
    }
  },
  methods: {
    update() {
      this.svg
        .selectAll("g.point")
        .data(this.model.Agents)
        .join(
          enter => {
            enter
              .append("g")
              .attr("class", "point")
              .call(g => {
                g.append("circle")
                  .attr("cx", d => this.x(d.PosX))
                  .attr("cy", d => this.y(d.PosY))
                  .attr("r", this.width / 100)
                  .attr("fill", "#FF0000");

                // g.append("line")
                //   .attr("y1", d => Math.max(0, this.y(d.Value.lower)))
                //   .attr("y2", d => Math.max(0, this.y(d.Value.upper)))
                //   .attr("x1", d => this.x(parseTime(d.Date)))
                //   .attr("x2", d => this.x(parseTime(d.Date)))
                //   .style("stroke", d => (d.Sign === "+" ? "red" : "green"));
              });
          },
          update => {
            update.call(g => {
              g.select("circle")
                .transition()
                .duration(300)
                .attr("cx", d => this.x(d.PosX))
                .attr("cy", d => this.y(d.PosY));
              //
              // g.select("line")
              //   .attr("x1", d => this.x(parseTime(d.Date)))
              //   .attr("x2", d => this.x(parseTime(d.Date)))
              //   .transition()
              //   .duration(300)
              //   .attr("y1", d => Math.max(0, this.y(d.Value.lower)))
              //   .attr("y2", d => this.y(d.Value.upper))
              //   .style("stroke", d => (d.Sign === "+" ? "red" : "green"));
            });
          },
          exit => {
            exit.transition(100).remove();
          }
        );
    }
  },
  mounted() {
    this.svg = d3
      .select("#" + this.vid)
      .append("svg")
      .style("width", "100%")
      .style("opacity", 0.6)
      .style("background-color", "#fff");

    this.width = this.svg.node().parentNode.clientWidth;
    this.height = this.svg.node().parentNode.clientHeight;

    this.svg.style("height", this.height);

    this.g = this.svg
      .append("g")
      .attr("transform", "translate(0,0)");

    this.x = d3
      .scaleLinear([0, 1])
      .range([0, this.width]);

    this.y = d3
      .scaleLinear([0, 1])
      .nice()
      .range([this.height, 0]);
  }
}

</script>
<style>
.vis-board {
  width: 100%;
  box-shadow: 0 0.5rem 2rem -1rem rgba(0, 0, 0, 0.1);
  grid-column: 1 / -1;
  align-self: center;
  display: grid;
  align-content: start;
  background-color: #ffffff;
  gap: 0.2rem;
  aspect-ratio: 1;
}

</style>