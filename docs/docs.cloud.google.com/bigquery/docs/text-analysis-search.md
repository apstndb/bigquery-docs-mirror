# Work with text analyzers

The [`  CREATE SEARCH INDEX  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_search_index_statement) , [`  SEARCH  ` function](/bigquery/docs/reference/standard-sql/search_functions) , and [`  TEXT_ANALYZE  ` function](/bigquery/docs/reference/standard-sql/text-analysis-functions#text_analyze) support advanced text analyzer configuration options. Understanding BigQuery's text analyzers and their options lets you refine your search experience.

This document provides an overview of the different text analyzers available in BigQuery and their configuration options, as well as examples of how text analyzers work with [search](/bigquery/docs/search) in BigQuery. For more information about text analyzer syntax, see [Text analysis](/bigquery/docs/reference/standard-sql/text-analysis) .

## Text analyzers

BigQuery supports the following text analyzers:

  - `  NO_OP_ANALYZER  `
  - `  LOG_ANALYZER  `
  - `  PATTERN_ANALYZER  `

### `     NO_OP_ANALYZER    `

Use the `  NO_OP_ANALYZER  ` when you have pre-processed data that you want to match exactly. There is no tokenization or normalization applied to the text. Since this analyzer does not perform tokenization or normalization, it accepts no configuration. For more information about `  NO_OP_ANALYZER  ` , see [`  NO_OP_ANALYZER  `](/bigquery/docs/reference/standard-sql/text-analysis#no_op_analyzer) .

### `     LOG_ANALYZER    `

The `  LOG_ANALYZER  ` modifies data in the following ways:

  - Text is made lowercase.

  - ASCII values greater than 127 are kept as is.

  - Text is split into individual terms called *tokens* by the following delimiters:
    
    ``` text
    [ ] < > ( ) { } | ! ; , ' " * & ? + / : = @ . - $ % \ _ \n \r \s \t %21 %26
    %2526 %3B %3b %7C %7c %20 %2B %2b %3D %3d %2520 %5D %5d %5B %5b %3A %3a %0A
    %0a %2C %2c %28 %29
    ```
    
    If you don't want to use the default delimiters, you can specify the delimiters you want to use as text analyzer options. `  LOG_ANALYZER  ` lets you configure specific delimiters and token filters for more control over your search results. For more information about the specific configuration options available when using the `  LOG_ANALYZER  ` , see [`  delimiters  ` analyzer option](/bigquery/docs/reference/standard-sql/text-analysis#log_analyzer_options) and [`  token_filters  ` analyzer option](/bigquery/docs/reference/standard-sql/text-analysis#token_filters_option) .

### `     PATTERN_ANALYZER    `

The `  PATTERN_ANALYZER  ` text analyzer extracts tokens from text using a regular expression. The regular expression engine and syntax used with `  PATTERN_ANALYZER  ` is [RE2](https://github.com/google/re2/) . `  PATTERN_ANALYZER  ` tokenizes patterns in the following order:

1.  It finds the first substring that matches the pattern (from the left) in the string. This is a token to be included in the output.
2.  It removes everything from the input string until the end of the substring found in step 1.
3.  It repeats the process until the string is empty.

The following table provides examples of `  PATTERN_ANALYZER  ` token extraction:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Pattern</th>
<th>Input text</th>
<th>Output tokens</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ab</td>
<td>ababab</td>
<td><ul>
<li>ab</li>
</ul></td>
</tr>
<tr class="even">
<td>ab</td>
<td>abacad</td>
<td><ul>
<li>ab</li>
</ul></td>
</tr>
<tr class="odd">
<td>[a-z]{2}</td>
<td>abacad</td>
<td><ul>
<li>ab</li>
<li>ac</li>
<li>ad</li>
</ul></td>
</tr>
<tr class="even">
<td>aaa</td>
<td>aaaaa</td>
<td><ul>
<li>aaa</li>
</ul></td>
</tr>
<tr class="odd">
<td>[a-z]/</td>
<td>a/b/c/d/e</td>
<td><ul>
<li>a/</li>
<li>b/</li>
<li>c/</li>
<li>d/</li>
</ul></td>
</tr>
<tr class="even">
<td>/[^/]+/</td>
<td>aa/bb/cc</td>
<td><ul>
<li>/bb/</li>
</ul></td>
</tr>
<tr class="odd">
<td>[0-9]+</td>
<td>abc</td>
<td></td>
</tr>
<tr class="even">
<td>(?:/?)[a-z]</td>
<td>/abc</td>
<td><ul>
<li>/abc</li>
</ul></td>
</tr>
<tr class="odd">
<td>(?:/)[a-z]</td>
<td>/abc</td>
<td><ul>
<li>/abc</li>
</ul></td>
</tr>
<tr class="even">
<td>(?:[0-9]abc){3}(?:[a-z]000){2}</td>
<td>7abc7abc7abcx000y000</td>
<td><ul>
<li>7abc7abc7abcx000y000</li>
</ul></td>
</tr>
<tr class="odd">
<td>".+"</td>
<td>"cats" and "dogs"</td>
<td><ul>
<li>"cats" and "dogs"</li>
</ul>
<br />
<br />
Note the use of <a href="https://stackoverflow.com/questions/2301285/what-do-lazy-and-greedy-mean-in-the-context-of-regular-expressions">greedy quantifiers +</a> makes the match to match the longest string possible in the text, causing '"cats" and "dogs"' to be extracted as a token in the text.</td>
</tr>
<tr class="even">
<td>".+?"</td>
<td>"cats" and "dogs"</td>
<td><ul>
<li>"cats"</li>
<li>"dogs"</li>
</ul>
<br />
<br />
Note the use of <a href="https://stackoverflow.com/questions/2301285/what-do-lazy-and-greedy-mean-in-the-context-of-regular-expressions">lazy quantifiers +?</a> makes the regular expression match the shortest string possible in the text, causing '"cats"', '"dogs"' to be extracted as 2 separate tokens in the text.</td>
</tr>
</tbody>
</table>

Using the `  PATTERN_ANALYZER  ` text analyzer gives you more control over the tokens extracted from a text when used with the [`  SEARCH  ` function](/bigquery/docs/reference/standard-sql/search_functions) . The following table shows how different patterns and results result in different `  SEARCH  ` results:

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Pattern</th>
<th>Query</th>
<th>Text</th>
<th>Tokens from text</th>
<th>SEARCH(text, query)</th>
<th>Explanation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>abc</td>
<td>abcdef</td>
<td>abcghi</td>
<td><ul>
<li>abcghi</li>
</ul></td>
<td>TRUE</td>
<td>'abc' in ['abcghi']</td>
</tr>
<tr class="even">
<td>cd[a-z]</td>
<td>abcdef</td>
<td>abcghi</td>
<td><ul>
<li>abcghi</li>
</ul></td>
<td>FALSE</td>
<td>'cde' in ['abcghi']</td>
</tr>
<tr class="odd">
<td>[a-z]/</td>
<td>a/b/</td>
<td>a/b/c/d/</td>
<td><ul>
<li>a/</li>
<li>b/</li>
<li>c/</li>
<li>d/</li>
</ul></td>
<td>TRUE</td>
<td>'a/' in ['a/', 'b/', 'c/', 'd/'] AND 'b/' in ['a/', 'b/', 'c/', 'd/']</td>
</tr>
<tr class="even">
<td>/[^/]+/</td>
<td>aa/bb/</td>
<td>aa/bb/cc/</td>
<td><ul>
<li>/bb/</li>
</ul></td>
<td>TRUE</td>
<td>'/bb/' in ['/bb/']</td>
</tr>
<tr class="odd">
<td>/[^/]+/</td>
<td>bb</td>
<td>aa/bb/cc/</td>
<td><ul>
<li>/bb/</li>
</ul></td>
<td>ERROR</td>
<td>No match found in query term</td>
</tr>
<tr class="even">
<td>[0-9]+</td>
<td>abc</td>
<td>abc123</td>
<td></td>
<td>ERROR</td>
<td>No match found in query term</td>
</tr>
<tr class="odd">
<td>[0-9]+</td>
<td>`abc`</td>
<td>abc123</td>
<td></td>
<td>ERROR</td>
<td>No match found in query term<br />
<br />
Matching backtick as backtick, not a special character.</td>
</tr>
<tr class="even">
<td>[a-z][a-z0-9]*@google\.com</td>
<td>This is my email: test@google.com</td>
<td>test@google.com</td>
<td><ul>
<li>test@google.com</li>
</ul></td>
<td>TRUE</td>
<td>'test@google.com' in 'test@google.com'</td>
</tr>
<tr class="odd">
<td>abc</td>
<td>abc\ abc</td>
<td>abc</td>
<td><ul>
<li>abc</li>
</ul></td>
<td>TRUE</td>
<td>'abc' in ['abc']<br />
<br />
Note that 'abc abc' is a single subquery(ie) after being parsed by the search query parser since the space is escaped.</td>
</tr>
<tr class="even">
<td>(?i)(?:Abc) (no normalization)</td>
<td>aBcd</td>
<td>Abc</td>
<td><ul>
<li>Abc</li>
</ul></td>
<td>FALSE</td>
<td>'aBc' in ['Abc']</td>
</tr>
<tr class="odd">
<td>(?i)(?:Abc)<br />
<br />
normalization:<br />
lower_case = true</td>
<td>aBcd</td>
<td>Abc</td>
<td><ul>
<li>abc</li>
</ul></td>
<td>TRUE</td>
<td>'abc' in ['abc']</td>
</tr>
<tr class="even">
<td>(?:/?)abc</td>
<td>bc/abc</td>
<td>/abc/abc/</td>
<td><ul>
<li>/abc</li>
</ul></td>
<td>TRUE</td>
<td>'/abc' in ['/abc']</td>
</tr>
<tr class="odd">
<td>(?:/?)abc</td>
<td>abc</td>
<td>d/abc</td>
<td><ul>
<li>/abc</li>
</ul></td>
<td>FALSE</td>
<td>'abc' in ['/abc']</td>
</tr>
<tr class="even">
<td>".+"</td>
<td>"cats"</td>
<td>"cats" and "dogs"</td>
<td><ul>
<li>"cats" and "dogs"</li>
</ul></td>
<td>FALSE</td>
<td>'"cats"' in ['"cats" and "dogs"]<br />
<br />
Note the use of <a href="https://stackoverflow.com/questions/2301285/what-do-lazy-and-greedy-mean-in-the-context-of-regular-expressions">greedy quantifiers +</a> makes the regular expression match the longest string possible in the text, causing '"cats" and "dogs"' to be extracted as a token in the text.</td>
</tr>
<tr class="odd">
<td>".+?"</td>
<td>"cats"</td>
<td>"cats" and "dogs"</td>
<td><ul>
<li>"cats"</li>
<li>"dogs"</li>
</ul></td>
<td>TRUE</td>
<td>'"cats"' in ['"cats"', '"dogs"]<br />
<br />
Note the use of <a href="https://stackoverflow.com/questions/2301285/what-do-lazy-and-greedy-mean-in-the-context-of-regular-expressions">lazy quantifiers +?</a> makes the regular expression match the shortest string possible in the text, causing '"cats"', '"dogs"' to be extracted as 2 separate tokens in the text.</td>
</tr>
</tbody>
</table>

## Examples

The following examples demonstrates the use of text analysis with customization options to create search indexes, extract tokens, and return search results.

### `     LOG_ANALYZER    ` with NFKC ICU normalization and stop words

The following example configures `  LOG_ANALYZER  ` options with [NFKC ICU](https://en.wikipedia.org/wiki/Unicode_equivalence) normalization and stop words. The example assumes the following data table with data already populated:

``` text
CREATE TABLE dataset.data_table(
  text_data STRING
);
```

To create a search index with NFKC ICU normalization and a list of stop words, create a JSON-formatted string in the `  analyzer_options  ` option of the [`  CREATE SEARCH INDEX  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_search_index_statement) . For a complete list of options available in when creating a search index with the `  LOG_ANALYZER  ` , see [`  LOG_ANALYZER  `](/bigquery/docs/reference/standard-sql/text-analysis#log_analyzer) . For this example, our stop words are `  "the", "of", "and", "for"  ` .

``` text
CREATE OR REPLACE SEARCH INDEX `my_index` ON `dataset.data_table`(ALL COLUMNS) OPTIONS(
  analyzer='PATTERN_ANALYZER',
  analyzer_options= '''{
    "token_filters": [
      {
        "normalizer": {
          "mode": "ICU_NORMALIZE",
          "icu_normalize_mode": "NFKC",
          "icu_case_folding": true
        }
      },
      { "stop_words": ["the", "of", "and", "for"] }
    ]
  }''');
```

Given the previous example, the following table describes the token extraction for various values of `  text_data  ` . Note that in this document the double question mark character ( *⁇* ) has been italicized to differentiate between two question marks (??):

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Data Text</th>
<th>Tokens for index</th>
<th>Explanation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>The Quick Brown Fox</td>
<td>["quick", "brown", "fox"]</td>
<td>LOG_ANALYZER tokenization produces the tokens ["The", "Quick", "Brown", "Fox"].<br />
<br />
Next, ICU normalization with <code dir="ltr" translate="no">       icu_case_folding = true      </code> lower cases the tokens to produce ["the", "quick", "brown", "fox"]<br />
<br />
Finally, the stop words filter removes "the" from the list.</td>
</tr>
<tr class="even">
<td>The Ⓠuick Ⓑrown Ⓕox</td>
<td>["quick", "brown", "fox"]</td>
<td>LOG_ANALYZER tokenization produces the tokens ["The", "Ⓠuick", "Ⓑrown", "Ⓕox"].<br />
<br />
Next, NFKC ICU normalization with <code dir="ltr" translate="no">       icu_case_folding = true      </code> lower cases the tokens to produce ["the", "quick", "brown", "fox"]<br />
<br />
Finally, the stop words filter removes "the" from the list.</td>
</tr>
<tr class="odd">
<td>Ⓠuick <em>⁇</em> Ⓕox</td>
<td>["quick??fox"]</td>
<td>LOG_ANALYZER tokenization produces the tokens ["The", "Ⓠuick <em>⁇</em> Ⓕox"].<br />
<br />
Next, NFKC ICU normalization with <code dir="ltr" translate="no">       icu_case_folding = true      </code> lower cases the tokens to produce ["quick??fox"]. Notice that the double question mark unicode has been normalized into 2 question mark ASCII characters.<br />
<br />
Finally, the stop words filter does nothing because none of the tokens are in the filter list.</td>
</tr>
</tbody>
</table>

Now that the search index has been created, you can use the [`  SEARCH  ` function](/bigquery/docs/reference/standard-sql/search_functions) to search the table using the same analyzer configurations specified in the search index. Note that if the analyzer configurations in the `  SEARCH  ` function don't match those of the search index, the search index won't be used. Use the following query:

``` text
SELECT
  SEARCH(
  analyzer => 'LOG_ANALYZER',
  analyzer_options => '''{
    "token_filters": [
      {
        "normalizer": {
          "mode": "ICU_NORMALIZE",
          "icu_normalize_mode": "NFKC",
          "icu_case_folding": true
        }
      },
      {
        "stop_words": ["the", "of", "and", "for"]
      }
    ]
  }''')
```

Replace the following:

  - `  search_query  ` : The text you want to search for.

The following table demonstrates various results based on different search text and different values of `  search_query  ` :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>text_data</th>
<th><code dir="ltr" translate="no">       search_query      </code></th>
<th>Result</th>
<th>Explanation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>The Quick Brown Fox</td>
<td><code dir="ltr" translate="no">       "Ⓠuick"      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
<td>The final list of tokens extracted from the text is ["quick", "brown", "fox"].<br />
The final list of tokens extracted from the text query is ["quick"].<br />
<br />
The list query tokens can all be found in the text tokens.</td>
</tr>
<tr class="even">
<td>The Ⓠuick Ⓑrown Ⓕox</td>
<td><code dir="ltr" translate="no">       "quick"      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
<td>The final list of tokens extracted from the text is ["quick", "brown", "fox"].<br />
The final list of tokens extracted from the text query is ["quick"].<br />
<br />
The list query tokens can all be found in the text tokens.</td>
</tr>
<tr class="odd">
<td>Ⓠuick <em>⁇</em> Ⓕox</td>
<td><code dir="ltr" translate="no">       "quick"      </code></td>
<td><code dir="ltr" translate="no">       FALSE      </code></td>
<td>The final list of tokens extracted from the text is ["quick??fox"].<br />
<br />
The final list of tokens extracted from the text query is ["quick"].<br />
<br />
"quick" is not in the list of tokens from the text.</td>
</tr>
<tr class="even">
<td>Ⓠuick <em>⁇</em> Ⓕox</td>
<td><code dir="ltr" translate="no">       "quick               ⁇              fox"      </code></td>
<td><code dir="ltr" translate="no">       TRUE      </code></td>
<td>The final list of tokens extracted from the text is ["quick??fox"].<br />
<br />
The final list of tokens extracted from the text query is ["quick??fox"].<br />
<br />
"quick??fox" is in the list of tokens from the text.</td>
</tr>
<tr class="odd">
<td>Ⓠuick <em>⁇</em> Ⓕox</td>
<td><code dir="ltr" translate="no">       "`quick               ⁇              fox`"      </code></td>
<td><code dir="ltr" translate="no">       FALSE      </code></td>
<td>In <code dir="ltr" translate="no">       LOG_ANALYZER      </code> , backtick requires exact text match.</td>
</tr>
</tbody>
</table>

### `     PATTERN_ANALYZER    ` for IPv4 search with stop words

The following example configures the `  PATTERN_ANALYZER  ` text analyzer to search for a specific pattern while filtering certain stop words. In this example, the pattern matches an IPv4 address and ignores the localhost value ( `  127.0.0.1  ` ).

This example assumes that the following table is populated with data:

``` text
CREATE TABLE dataset.data_table(
  text_data STRING
);
```

To create a search index the `  pattern  ` option and a list of stop words, create a JSON-formatted string in the `  analyzer_options  ` option of the [`  CREATE SEARCH INDEX  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_search_index_statement) . For a complete list of options available in when creating a search index with the `  PATTERN_ANALYZER  ` , see [`  PATTERN_ANALYZER  `](/bigquery/docs/reference/standard-sql/text-analysis#pattern_analyzer) . For this example, our stop words are the localhost address, `  127.0.0.1  ` .

``` text
CREATE SEARCH INDEX my_index
ON dataset.data_table(text_data)
OPTIONS (analyzer = 'PATTERN_ANALYZER', analyzer_options = '''{
  "patterns": [
    "(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)[.]){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)"
  ],
  "token_filters": [
    {
      "stop_words": [
        "127.0.0.1"
      ]
    }
  ]
}'''
);
```

When using regular expressions with `  analyzer_options  ` , include three leading `  \  ` symbols to properly escape regular expressions that include a `  \  ` symbol, such as `  \d  ` or `  \b  ` .

The following table describes the tokenization options for various values of `  text_data  `

<table>
<thead>
<tr class="header">
<th>Data Text</th>
<th>Tokens for index</th>
<th>Explanation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>abc192.168.1.1def 172.217.20.142</td>
<td>["192.168.1.1", "172.217.20.142"]</td>
<td>The IPv4 patterns capture the IPv4 addresses even if there's no space between the address and the text.</td>
</tr>
<tr class="even">
<td>104.24.12.10abc 127.0.0.1</td>
<td>["104.24.12.10"]</td>
<td>"127.0.0.1" is filtered out since it's in the list of stop words.</td>
</tr>
</tbody>
</table>

Now that the search index has been created, you can use the [`  SEARCH  ` function](/bigquery/docs/reference/standard-sql/search_functions) to search the table based on the tokenization specified in `  analyzer_options  ` . Use the following query:

``` text
SELECT
  SEARCH(dataset.data_table.text_data
  "search_data",
  analyzer => 'PATTERN_ANALYZER',
  analyzer_options => '''{
    "patterns": [
      "(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)[.]){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)"
      ],
    "token_filters": [
      {
        "stop_words": [
          "127.0.0.1"
        ]
      }
    ]
  }'''
);
```

Replace the following:

  - `  search_query  ` : The text you want to search for.

The following table demonstrates various results based on different search text and different values of `  search_query  ` :

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>text_data</th>
<th><code dir="ltr" translate="no">       search_query      </code></th>
<th>Result</th>
<th>Explanation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>128.0.0.2</td>
<td>"127.0.0.1"</td>
<td>ERROR</td>
<td>No search token in query.<br />
<br />
The query goes through the text analyzer, which filters out the "127.0.0.1" token.</td>
</tr>
<tr class="even">
<td>abc192.168.1.1def 172.217.20.142</td>
<td>"192.168.1.1abc"</td>
<td>TRUE</td>
<td>The list of tokens extracted from the query is ["192.168.1.1"].<br />
<br />
The list of tokens extracted from text is ["192.168.1.1", "172.217.20.142"].</td>
</tr>
<tr class="odd">
<td>abc192.168.1.1def 172.217.20.142</td>
<td>"`192.168.1.1`"</td>
<td>TRUE</td>
<td>The list of tokens extracted from the query is ["192.168.1.1"].<br />
<br />
The list of tokens extracted from text is ["192.168.1.1", "172.217.20.142"].<br />
<br />
Note that backticks are treated as regular characters for PATTERN_ANALYZER.</td>
</tr>
</tbody>
</table>

## What's next

  - For an overview of search index use cases, pricing, required permissions, and limitations, see the [Introduction to search in BigQuery](/bigquery/docs/search-intro) .
  - For information about efficient searching of indexed columns, see [Search with an index](/bigquery/docs/search) .
