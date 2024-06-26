# sis-extras

## Overview
The `sis-extras` package provides a set of Python utilities designed to help you develop beautiful, performant streamlit-in-snowflake apps.

Currently, this package includes modules for managing database connections (`connection.py`) and creating interactive data tiles (`formatting.py`).

## Installation
To install `sis-extras`, you can use pip:

```bash
pip install sis-extras
```

## Modules

### connection.py
This module handles connections to Snowflake databases, providing functionality to manage sessions and execute SQL queries directly, returning results in a Pandas DataFrame format.

#### Key Functions:
- **`SnowparkConnection`**: Manages Snowflake database connections.
- **`get_data_frame_from_raw_sql`**: Executes a SQL query and returns the results as a Pandas DataFrame.
- **`get_pandas_df`**: Converts a Snowpark DataFrame to a Pandas DataFrame.
- **`join_cached`**: Provides a cached mechanism for joining two Snowpark DataFrames.

### formatting.py
This module aids in the visualization of data using Streamlit, Altair, and Plotly, focusing on creating interactive tiles that can display data, charts, and SQL queries.

#### Key Functions:
- **`tile`**: Creates a tile in Streamlit that can display a chart, data preview, SQL query, and a description.
- **`tile_ctx`**: A context manager version of `tile` for more flexible content management within a tile.
- **`altair_time_series`**: Generates a time series chart using Altair, designed to handle specific formatting and tooltip requirements.


## Usage Examples

### Using SnowparkConnection

```python
from sis_extras.connection import get_table, get_data_frame_from_raw_sql, get_pandas_df

# Use Snowpark API

table = get_table("your_table").limit(10)

table_pd = get_pandas_df(table)

st.write(table_pd)

# Use SQL

table_pd = get_data_frame_from_raw_sql("SELECT * FROM your_table")

st.write(table_pd)
```


### Creating a Data Tile

```python
from sis_extras.formatting import tile
import pandas as pd
import altair as alt

# Sample DataFrame

data = pd.DataFrame({
    'x': range(10),
    'y': range(10)
})

# Sample Chart

chart = alt.Chart(data).mark_line().encode(
    x='x',
    y='y'
)

# Create a tile with data and chart

tile(data, "Sample Tile", chart=chart, sql="SELECT x, y FROM your_table")
```

![Shows a tile with data and chart](images/example_tile.png)
