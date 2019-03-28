#wrapper {
  font-family: Palatino, Georgia, "Times New Roman", serif;
  font-weight: normal;
  font-size: 0.8764em;
  line-height: 1.5em;
  margin: 0;
  font-size: 14px; }
  #wrapper p {
    margin: 1.3125em 0;
    font-size: 1.1429em;
    line-height: 1.6125em; }
  #wrapper ul {
    list-style: square; }
  #wrapper ol {
    list-style: decimal; }
  #wrapper ul, #wrapper ol {
    padding-left: 0;
    list-style-position: outside; }
    #wrapper ul li, #wrapper ol li {
      font-size: 110%;
      line-height: 1.525em; }
      #wrapper ul li li, #wrapper ol li li {
        font-size: 100%; }
      #wrapper ul li p, #wrapper ol li p {
        font-size: 100%;
        margin-left: 1em; }
    #wrapper ul ul, #wrapper ul ol, #wrapper ol ul, #wrapper ol ol {
      margin-bottom: .4em;
      padding-left: 30px; }
    #wrapper ul ul, #wrapper ol ul {
      list-style: circle; }
  #wrapper strong {
    font-weight: bold; }
  #wrapper em {
    font-style: italic; }
  #wrapper h1 {
    margin: 0.6563em 0;
    font-size: 2.8em;
    line-height: 1.6563em; }
  #wrapper h2 {
    margin: 0.875em 0;
    font-size: 1.7143em;
    line-height: 0.875em; }
  #wrapper h3 {
    margin: 1em 0;
    font-size: 1.5em;
    line-height: 1em; }
  #wrapper h4 {
    margin: 1.1667em 0;
    font-size: 1.2857em;
    line-height: 1.1667em; }
  #wrapper h5 {
    margin: 1.3125em 0;
    font-size: 1.1429em;
    line-height: 1.3125em; }
  #wrapper h6 {
    margin: 1.5em 0;
    font-size: 1em;
    line-height: 1.5em; }
  #wrapper h1, #wrapper h2, #wrapper h3, #wrapper h4, #wrapper h5, #wrapper h6 {
    font-weight: bold; }
    #wrapper h1 a, #wrapper h2 a, #wrapper h3 a, #wrapper h4 a, #wrapper h5 a, #wrapper h6 a {
      color: #514d3f;
      border-bottom: dotted 1px #a7a099; }
      #wrapper h1 a:hover, #wrapper h2 a:hover, #wrapper h3 a:hover, #wrapper h4 a:hover, #wrapper h5 a:hover, #wrapper h6 a:hover {
        color: #13120f; }
  #wrapper h1, #wrapper h2 {
    padding-bottom: .4em;
    padding-top: .25em;
    font-family: "Hoefler Text", Georgia, serif;
    line-height: 1.5em;
    color: #514d3f;
    text-shadow: 1px 0px 0px #a7a099, 0 1px 0 white; }
  #wrapper h1 {
    text-align: center; }
    #wrapper h1:before {
      content: "\0360";
      position: relative;
      left: -30px;
      top: .4em;
      color: #837e70;
      text-shadow: 1px 0px 0px #a7a099, 0 1px 0 white; }
    #wrapper h1:after {
      content: "\0360";
      position: relative;
      right: -30px;
      top: .4em;
      color: #837e70;
      text-shadow: 1px 0px 0px #a7a099, 0 1px 0 white; }
  #wrapper h2 {
    box-shadow: 0 -1px 0 white, 0 -2px 0 #837e70;
    margin-top: 1em;
    padding-bottom: 0; }
  #wrapper, #wrapper p, #wrapper td, #wrapper div {
    color: #45462f;
    word-wrap: break-word;
    -webkit-font-smoothing: antialiased; }
  #wrapper a {
    color: #00857a;
    text-decoration: none;
    -webkit-transition: color 0.1s ease-in-out;
    -moz-transition: color 0.1s ease-in-out;
    -o-transition: color 0.1s ease-in-out;
    -ms-transition: color 0.1s ease-in-out;
    transition: color 0.1s ease-in-out; }
    #wrapper a:hover {
      color: #35b8ad; }
  #wrapper strong {
    font-weight: 600;
    color: #605b4b; }
  #wrapper .footnote {
    font-size: .8em;
    vertical-align: super;
    color: #0d6ea1; }
  #wrapper img {
    max-width: 100%;
    height: auto;
    border: solid 2px rgba(56, 40, 18, 0.25); }
  #wrapper dt {
    font-weight: bold; }
  #wrapper dd {
    margin-bottom: 1em;
    text-indent: 1em; }
  #wrapper blockquote {
    margin: 14px 40px; }
  #wrapper code {
    font-family: courier, monospace;
    background: #f2ede8;
    border: solid 1px #a7a099;
    font-size: .95em; }
  #wrapper pre {
    background: #f2ede8;
    padding: 4px; }
  #wrapper pre code {
    font-size: 1em;
    margin: 0;
    padding: 4px;
    border: none;
    background: none; }
  #wrapper hr {
    border-color: #f2ede8;
    height: 0;
    background-color: #a7a099; }

@media print {
  body {
    overflow: auto;
    background: #fff;
    color: #000 !important; }

  img, pre, blockquote, table, figure {
    page-break-inside: avoid; }

  #wrapper {
    background: #fff;
    position: relative;
    color: #000;
    text-indent: 0px;
    padding: 1in;
    font-size: 85%; } }
@media screen {
  body {
    height: 100%;
    background: #f0edeb; }

  #wrapper {
    color: #514d3f;
    overflow: auto;
    text-indent: 0px;
    padding: 25px; }
    #wrapper ::selection {
      background: rgba(157, 193, 200, 0.5); }
    #wrapper h1::selection, #wrapper h2::selection, #wrapper h3::selection, #wrapper h4::selection, #wrapper h5::selection, #wrapper h6::selection {
      background-color: rgba(133, 201, 232, 0.3); }
    #wrapper code::selection {
      background-color: rgba(0, 0, 0, 0.7);
      color: #eee; }
    #wrapper code span::selection {
      background-color: rgba(0, 0, 0, 0.7) !important;
      color: #eee !important; }
    #wrapper a::selection {
      background-color: rgba(255, 230, 102, 0.2); }
    #wrapper td::selection, #wrapper th::selection, #wrapper caption::selection {
      background-color: rgba(180, 237, 95, 0.5); }

  .inverted {
    background: #39362f; }
    .inverted #wrapper {
      background: #39362f; }
      .inverted #wrapper a::selection {
        background-color: rgba(255, 230, 102, 0.6); }
      .inverted #wrapper p, .inverted #wrapper td, .inverted #wrapper li, .inverted #wrapper h1, .inverted #wrapper h2, .inverted #wrapper h3, .inverted #wrapper h4, .inverted #wrapper h5, .inverted #wrapper h6, .inverted #wrapper pre, .inverted #wrapper code, .inverted #wrapper th, .inverted #wrapper hr, .inverted #wrapper strong, .inverted #wrapper em, .inverted #wrapper .math, .inverted #wrapper dd, .inverted #wrapper dt {
        color: #f0ede3;
        border-color: #423d2f;
        background: #39362f; }
      .inverted #wrapper hr {
        border-color: rgba(52, 52, 52, 0.3); }
      .inverted #wrapper a {
        color: #fff;
        text-decoration: underline;
        border-bottom: none; }
      .inverted #wrapper .popup li, .inverted #wrapper .popup ul, .inverted #wrapper .popup strong {
        background: none; } }
#wrapper li > p:first-child {
  margin: 0; }
#wrapper li p {
  margin: .5em 0; }
#wrapper caption, #wrapper col, #wrapper colgroup, #wrapper table, #wrapper tbody, #wrapper td, #wrapper tfoot, #wrapper th, #wrapper thead, #wrapper tr {
  border-spacing: 0; }
#wrapper caption {
  display: table-caption;
  font-weight: bold; }
#wrapper col {
  display: table-column; }
#wrapper colgroup {
  display: table-column-group; }
#wrapper tbody {
  display: table-row-group; }
#wrapper tfoot {
  display: table-footer-group; }
#wrapper thead {
  display: table-header-group; }
#wrapper td, #wrapper th {
  display: table-cell; }
#wrapper th {
  font-weight: bold; }
#wrapper tr {
  display: table-row; }
#wrapper table {
  display: table;
  table-layout: fixed;
  border-collapse: collapse;
  empty-cells: hide;
  margin: 0 0 24px 0;
  padding: 0;
  border: 0;
  margin-top: -1px;
  margin-bottom: 23px;
  border: 1px solid rgba(124, 119, 112, 0.5); }
  #wrapper table th, #wrapper table td {
    padding: 0 1em;
    font-size: 1.1em;
    line-height: 23px; }
  #wrapper table tbody {
    background-color: rgba(124, 119, 112, 0.05); }
  #wrapper table thead, #wrapper table tfoot {
    background-color: rgba(124, 119, 112, 0.15); }
  #wrapper table tr:nth-child(odd) {
    background-color: rgba(227, 217, 205, 0.06); }
  #wrapper table tr:nth-child(even),
  #wrapper table td:nth-child(even) {
    background-color: rgba(124, 119, 112, 0.06); }
  #wrapper table thead,
  #wrapper table tfoot {
    border: 1px solid rgba(124, 119, 112, 0.5);
    border-bottom: 1px solid rgba(124, 119, 112, 0.2); }
  #wrapper table thead tr th:last-child {
    border-right: 1px solid rgba(124, 119, 112, 0.5); }
#wrapper figure {
  position: relative;
  display: inline-block;
  margin-bottom: 2em; }
  #wrapper figure:hover {
    cursor: pointer; }
#wrapper figcaption {
  text-align: center;
  position: absolute;
  background: transparent;
  width: 100%;
  left: 0;
  bottom: -20px;
  color: #a7a099; }
#wrapper .poetry pre {
  font-family: Georgia, Garamond, serif !important;
  font-style: italic;
  font-size: 110% !important;
  line-height: 1.6em;
  display: block;
  margin-left: 1em; }
  #wrapper .poetry pre code {
    font-family: Georgia, Garamond, serif !important;
    word-break: break-all;
    word-break: break-word;
    /* Non standard for webkit */
    -webkit-hyphens: auto;
    -moz-hyphens: auto;
    hyphens: auto;
    white-space: pre-wrap; }
#wrapper sup, #wrapper sub, #wrapper a.footnote {
  font-size: 1.4ex;
  height: 0;
  line-height: 1;
  vertical-align: super;
  position: relative; }
#wrapper sub {
  vertical-align: sub;
  top: -1px; }

## Java Essentials For Basic Data Analysis
### Table of Contents

#### CHAPTER 1 : Introduction
1. [Java Data Collection](./datacoolection.md)
2. [Exception Handling](./exception.md)

#### CHAPTER 2 : Getting Data Into and Out of Java
2. [Data Frame](./dataframe.md)
2. [File Format](./fileformat.md)
   1. [CSV](./README.md)
   2. [Excel](./README.md)
   3. [Pdf](./README.md)
   4. [SQL](./README.md)   
   5. [JSON](./README.md)
3. [Implement Inheritance](./README.md)
4. [Prepairing Data](./README.md)
   1. [Cleaning Data](./README.md)
   2. [Creating New Var](./README.md)
   3. [Organizing Data](./README.md)
   4. [Agregat Statistik Analysis Computing](./README.md)
   5. [Case Study](./README.md)
5. [Mid Test](./README.md)
#### CHAPTER 3 : Finding Meaning
1. [Sorting](./README.md)
2. [Correlation](./README.md)
3. [Implement Polymorphism](./README.md)                                               
4. [Regression](./README.md)
5. [Pivot Table](./README.md)
6. [Visualizing Data](./README.md)
#### CHAPTER 4: Social Media Connection
1. Twitter
2. [Wikipedia](./README.md)
3. [Youtube](./README.md)
4. Facebook
5. Instagram
6. [Case Study](./README.md)

