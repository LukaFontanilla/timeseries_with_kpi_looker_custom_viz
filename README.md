# Time Series Aggregate Visualization for Looker

This custom visualization plugin provides an interactive time series chart with a prominent display of an aggregated value using various aggregation functions (average, sum, median, min, max). It is designed for easy integration with [Looker](https://looker.com/) dashboards and dynamically loads [Chart.js](https://www.chartjs.org/) for rendering.

## Features

- **Dynamic Aggregation**: Choose from average, sum, median, min, or max for your time series metric.
- **Customizable Display**: Prominent, formatted aggregate value above the chart.
- **Interactive Line Chart**: Visualize your measure over time with a responsive Chart.js-powered chart.
- **Looker Format String Support**: Aggregated value formatting supports Looker value format strings.
- **Configurable Options**: Select aggregation type and chart color directly from the visualization options menu.

## Demo

![Demo Custom Viz](/viz-demo.png)

## How It Works

1. **Loads Chart.js from CDN** dynamically in the browser.
2. **Renders a large aggregate value** at the top, calculated over your selected measure using your chosen aggregation.
3. **Displays a time series line chart** for your selected measure, using the first dimension as the time axis.
4. **Formatting and styling** use inlined CSS for a modern, clean appearance.

## Usage

### 1. Install the Visualization

- Upload the visualization code as a [custom visualization in a LookML project](https://cloud.google.com/looker/docs/reference/param-manifest-visualization).
- Or add the JavaScript code to a public CDN and [configure that visualization in Looker Admin](https://cloud.google.com/looker/docs/admin-panel-platform-visualizations).

### 2. Configure Your Looker Query

- Include **at least one dimension** (preferably a time/date field).
- Include **at least two measures** (numeric field).
- The visualization uses:
  - The **first dimension** as the X (time) axis.
  - The **first and second measures** for the chart and aggregation (see limitations).

### 3. Visualization Options

| Option                     | Description                                            | Default        |
|----------------------------|--------------------------------------------------------|----------------|
| Aggregation Function       | Choose avg, sum, median, min, max                      | avg            |
| Chart Line Color           | Select chart line color (hex)                          | #1F77B4        |
| Aggregated Value Format    | Looker value format string for the displayed aggregate | #,##0.00       |

## Code Overview

- **Dynamic Script Loading**: Chart.js is loaded from CDN at runtime.
- **Aggregation Functions**: `avg`, `sum`, `median`, `min`, `max` are selectable.
- **UI Structure**: Uses a flexbox container with styled elements for value and chart.
- **Looker Integration**: Uses Looker's plugin API to register the visualization and handle data updates.

## Limitations

- Requires at least **one dimension** and **two measures**.
- The first dimension and first two measures in the Looker query are used (can be customized in code).
- Aggregation is always calculated on the **second measure**, while the chart shows the **first measure**.

## Customization

- Modify the `aggregationFunctions` object to add more aggregation methods.
- Update the CSS in the `css` variable to tweak the appearance.
- Customize the Chart.js options for different chart types or interactions.

## Dependencies

- [Chart.js 4.4.0 (UMD)](https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js) (loaded dynamically)
