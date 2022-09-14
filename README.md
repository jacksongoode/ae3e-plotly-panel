# Plotly Panel

[![Marketplace](https://img.shields.io/badge/dynamic/json?logo=grafana&color=F47A20&label=marketplace&prefix=v&query=%24.items%5B%3F%28%40.slug%20%3D%3D%20%22grafana-plotly-plugin%22%29%5D.version&url=https%3A%2F%2Fgrafana.com%2Fapi%2Fplugins)](https://grafana.com/grafana/plugins/jacksongoode-plotly-plugin)
[![Downloads](https://img.shields.io/badge/dynamic/json?logo=grafana&color=F47A20&label=downloads&query=%24.items%5B%3F%28%40.slug%20%3D%3D%20%22grafana-plotly-plugin%22%29%5D.downloads&url=https%3A%2F%2Fgrafana.com%2Fapi%2Fplugins)](https://grafana.com/grafana/plugins/jacksongoode-plotly-plugin)

Render charts with [Plotly.js](https://plotly.com/javascript/). A maintained fork of [this plugin](https://github.com/ae3e/ae3e-plotly-panel):

- Plotly.js library updated
- Dependencies updated
- Grafana version support updated
- Annotation support added
- Depreciated packages/code removed
- Linting, style standardization, code correction
- Better documentation

Unlike the [natel-plotly-panel](https://github.com/NatelEnergy/grafana-plotly-plugin), this plugin is not limited to specific types of charts. This plugin allows fine grained control over the `data`, `layout`, and`config` parameters used to build a Plotly plot.

## Getting started

The _Data_, _Layout_ and _Config_ fields match the common parameters described in [Plotly's documentation](https://plotly.com/javascript/plotlyjs-function-reference/). They must be in JSON format.

Data provided by the data source can be transformed via a user-defined script before to be injected in the Plotly chart. The script includes 2 arguments:

- `data`: Data returns by the datasource. See the example below for the object's schema.
- `variables`: Object that contains [Grafana's variables](https://grafana.com/docs/grafana/latest/variables/) available in the current dashboard (user variables and few global variables: `__from`, `__to`, `__interval` and `__interval_ms`).

The script must return an object with one or more of the following properties:

- `data`
- `layout`
- `config`
- `frames`

For example:

```javascript
let x = data.series[0].fields[0].values.buffer;
let y = data.series[0].fields[1].values.buffer;

let series = {
  x: x,
  y: y,
  name: variables.project // where 'project' is the name of a Grafana's variable
};

return {
  data: [series],
  config: {
    displayModeBar: false,
  },
};
```
