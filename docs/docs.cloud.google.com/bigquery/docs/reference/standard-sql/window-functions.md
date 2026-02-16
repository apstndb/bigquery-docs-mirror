GoogleSQL for BigQuery supports the following [window functions](/bigquery/docs/reference/standard-sql/window-function-calls) .

## Function list

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Summary</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#cume_dist"><code dir="ltr" translate="no">        CUME_DIST       </code></a></td>
<td>Gets the cumulative distribution (relative position (0,1]) of each row within a window.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/numbering_functions">Numbering functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#dense_rank"><code dir="ltr" translate="no">        DENSE_RANK       </code></a></td>
<td>Gets the dense rank (1-based, no gaps) of each row within a window.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/numbering_functions">Numbering functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#first_value"><code dir="ltr" translate="no">        FIRST_VALUE       </code></a></td>
<td>Gets a value for the first row in the current window frame.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/navigation_functions">Navigation functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#lag"><code dir="ltr" translate="no">        LAG       </code></a></td>
<td>Gets a value for a preceding row.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/navigation_functions">Navigation functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#last_value"><code dir="ltr" translate="no">        LAST_VALUE       </code></a></td>
<td>Gets a value for the last row in the current window frame.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/navigation_functions">Navigation functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#lead"><code dir="ltr" translate="no">        LEAD       </code></a></td>
<td>Gets a value for a subsequent row.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/navigation_functions">Navigation functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#nth_value"><code dir="ltr" translate="no">        NTH_VALUE       </code></a></td>
<td>Gets a value for the Nth row of the current window frame.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/navigation_functions">Navigation functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#ntile"><code dir="ltr" translate="no">        NTILE       </code></a></td>
<td>Gets the quantile bucket number (1-based) of each row within a window.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/numbering_functions">Numbering functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#percent_rank"><code dir="ltr" translate="no">        PERCENT_RANK       </code></a></td>
<td>Gets the percentile rank (from 0 to 1) of each row within a window.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/numbering_functions">Numbering functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#percentile_cont"><code dir="ltr" translate="no">        PERCENTILE_CONT       </code></a></td>
<td>Computes the specified percentile for a value, using linear interpolation.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/navigation_functions">Navigation functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/navigation_functions#percentile_disc"><code dir="ltr" translate="no">        PERCENTILE_DISC       </code></a></td>
<td>Computes the specified percentile for a discrete value.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/navigation_functions">Navigation functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#rank"><code dir="ltr" translate="no">        RANK       </code></a></td>
<td>Gets the rank (1-based) of each row within a window.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/numbering_functions">Numbering functions</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/numbering_functions#row_number"><code dir="ltr" translate="no">        ROW_NUMBER       </code></a></td>
<td>Gets the sequential row number (1-based) of each row within a window.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/numbering_functions">Numbering functions</a> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/geography_functions#st_clusterdbscan"><code dir="ltr" translate="no">        ST_CLUSTERDBSCAN       </code></a></td>
<td>Performs DBSCAN clustering on a group of <code dir="ltr" translate="no">       GEOGRAPHY      </code> values and produces a 0-based cluster number for this row.<br />
For more information, see <a href="/bigquery/docs/reference/standard-sql/geography_functions">Geography functions</a> .</td>
</tr>
</tbody>
</table>
