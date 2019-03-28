# DataFrame 

1. [Introduction](#Introduction)
2. [Tables and Columns](#Tables-and-Columns)
3. [Selections](#Selections)
4. [Tables](#Tables)
5. [Exercise](#Exercise)

## Introduction
---------------
**DataFrame** is a 2-dimensional labeled data structure with columns of potentially different types. You can think of it like a spreadsheet or SQL table, or a dict of Series objects. It is generally the most commonly used pandas object.
Like Series, DataFrame accepts many different kinds of input:

* Dict of 1D arrays, hash, or vector
* Structured or record array
* Another DataFrame

Along with the data, you can optionally pass index (row labels) and columns (column labels) arguments. If you pass an index and / or columns, you are guaranteeing the index and / or columns of the resulting DataFrame. Thus, a dict of Series plus a specific index will discard all data not matching up to the passed index.
If axis labels are not passed, they will be constructed from the input data based on common sense rules.

## Tables and Columns
---------------
As you would expect, DataFrame is all about tables, and tables are made of columns. We’ll start with columns.
### Columns
A column is a named, one-dimensional collection of data. It may or may not be part of a table. All data in a column must be of the same type.

Table DataFrame supports columns for Strings, doubles, booleans, LocalDates, LocalTimes, and LocalDateTimes. The date and time columns are comparable with the java.time classes introduced in Java 8.

To create a column you can use one of its static create() methods:

``` javascript
public static void main(String[] args) throws Exception{

	double[] numbers = {1, 2, 3, 4};
	DoubleColumn nc = DoubleColumn.create("Test", numbers);
	System.out.println(nc.print());

}
``` 
**Output:**
```
	Column: Test
	1.0
	2.0
	3.0
	4.0
``` 
Each column has an associated 0-based index. To get an individual value call get() with the index.
```
	nc.get(2);
```
which returns 3.0.

### Array Operations
Table DataFrame makes columns easy to work with. Operations that work on numbers in standard Java, for example, often work on columns of numbers in Table DataFrame. To multiply every value in a column by 4, we use the multiply() method, which returns a new column like the original.
```
   DoubleColumn nc2 = nc.multiply(4);
   System.out.println(nc2.print());
```
**Output:**
```
	Column: Test * 4.0
	4.0
	8.0
	12.0
	16.0
```
As you can see, the values are 4x the values in the original. The new column’s name is made by combining the original “Test” and the operation (* 4). You can change it if you like using ``setName(aString)``.

There are so many columnar operations in Table DataFrame that, as a general rule, if you find yourself writing a for loop to process a column or table, you may be missing something.

### Objects and Primitives
Many Java programs and programmers work exclusively with Objects, rather than primitives. In **Java DataFrame**, we use primitives whenever possible because they use much less memory than their boxed alternatives. A Byte object, for example, uses as much memory as a primitive double, even though bytes have a range of only 256 values.

There is a price for this frugality. When you work with primitives, you forgo some common java capabilities, like the use of standard Java 8 predicates. While Java thoughtfully provides some specialized predicate interfaces (e.g. IntPredicate), they don’t provide any primitive BiPredicate implementations, nor do their primitive interfaces cover all primitive types. Without an IntBiPredicate, we can’t implement operations like a < b. So we were left to roll our own. You can find them in the package tech.tablesaw.filtering.predicates. They work like the standard objects.

## Selections
---------------
Before going on to tables, we should talk about selections. Selections are used to filter both tables and columns. Often they work behind the scenes, but you can use them directly. For example, consider our ``DoubleColumn`` containing the values {1, 2, 3, 4}. You can filter that column by sending it a message. For example:
```
	nc.isLessThan(3);
```
This operation returns a Selection. Logically, it’s a bitmap of the same size as the original column. The method above, effectively, returns 1, 1, 0, 0, since the first two values in the column are less than three, and the last two are not.

What you probably wanted was not a Selection object, but a new DoubleColumn that contains only the values that passed the filter. To get this, you use the where(aSelection) method to apply the selection:

```
  DoubleColumn filtered = nc.where(nc.isLessThan(3));
  > Column: Test < 3.0
  1.0
  2.0
```
Doing this in two steps provides many benefits. For one, it lets us combine filters. For example:
```
  DoubleColumn filtered = nc.where(nc.isLessThan(3).and(nc.isOdd());
```
If the methods returned columns directly, they couldn’t be combined this way. It also lets us use the same method for filtering both tables and columns, as you’ll see below.

### Selecting by index
These examples show how to select using predicates. You can also use a selection to retrieve the value at a specific index, or indexes. All of the following are supported:
```
  nc.where(Selection.with(0, 2));  	// returns 2 rows with the given indexes
  nc.where(Selection.selectNRowsAtRandom(2)); // returns 2 randomly selected rows
  nc.where(Selection.withRange(1, 3));		// returns rows 1-3 inclusive
  nc.where(Selection.withoutRange(1, 3));		// returns row 0
```
If you have several columns of the same length as you would in a table of data, you can make a selection with one column and use it to filter another:

```
   DoubleColumn result = firstColumn.where(someOtherColumn.startsWith("foo"));
```

>> **Key point:** Note the methods ``startsWith(aString)``,  ``isLessThan(aNumber)``, and ``isOdd()``. These were predefined for your use. There are many such methods that can be used in building queries. For StringColumn, they’re defined in the ``tech.tablesaw.columns.strings.StringFilters interface``. It also includes ``endsWith()``, ``isEmpty()``, ``isAlpha()``, containsString()1, etc. Each column has a similar set of filter operations. They can all be found in the filter interfaces located in sub-folders of tech.tablesaw.columns (e.g. ``tech.tablesaw.columns.dates.DateFilters``).


## Tables
---------------
A table is a named collection of columns. All columns in the table must have the same number of elements, although missing values are allowed. A table can contain any combination of column types.

### Creating Tables
You can create a table in code. Here we create a table and add two new columns to it:
```
   String[] animals = {"bear", "cat", "giraffe"};
   double[] cuteness = {90.1, 84.3, 99.7};
   Table cuteAnimals = Table.create("Cute Animals")
	    .addColumns(
		   StringColumn.create("Animal types", animals),
		   DoubleColumn.create("rating", cuteness));
```		   
### Importing data
More frequently, you will load a table from a CSV or other delimited text file.
```
Table x = Table.read().csv("data/gradedata.csv");
```

**Java DataFrame** does a pretty good job at guessing the column types for many data sets, but you can specify them if it guesses wrong, or to improve performance. Numerous other options are available, such as specifying whether or not there’s a header, using a non-standard delimiter, supplying a custom missing value indicator, and so on.

**Note:** Getting data loaded is sometimes the hardest part of data analysis. Advanced options for loading data are described in the documentation on Importing Data. That section also shows how you can read data from a database, a stream, or an HTML table. The stream interfaces lets you read data from a Web site or an S3 bucket.

### Exploring Tables
Because **Java DataFrame** excels at manipulating tables, we use them whenever we can. When you ask **Java DataFrame** for the structure of a table, the answer comes back in the form of another table where one column contains the column names, etc. The structure() method is one of several that help you to know a new data set. Here are some examples.
```
Table structure = bushTable.structure();

>	          Structure of gradedata.csv          

 Index  |   Column Name    |  Column Type  |
--------------------------------------------
     0  |           fname  |       STRING  |
     1  |           lname  |       STRING  |
     2  |          gender  |       STRING  |
     3  |             age  |        SHORT  |
     4  |        exercise  |        SHORT  |
     5  |           hours  |        SHORT  |
     6  |           grade  |        FLOAT  |
     7  |  addressMarcia   |       STRING  |
		 
String shape = bushTable.shape();
>	1999 rows X 8 cols

Table head = bushTable.first(2);
>	             gradedata.csv              

	fname   |   lname    |  gender  |  age  |	 
	-----------------------------------
    Kadeem  |  Morrison  |    male  |   18  |
    Linus   |    Morris  |    male  |   19  |	
	
Table tail = myTable.last(3);
> etc.
```
Table’s ``toString()`` method returns a String representation like those shown above. It returns a limited number of rows by default, but you can also use ``table.printAll()``, or ``table.print(n)`` to get the output you want.

Of course, this is just the beginning of exploratory data analysis. You can also use numeric and visual tools to explore your data. These facilities are described in the documentation on statistics and plotting, respectively.

### Working with a table’s columns
Often you’ll work with specific columns in a table. Here are some useful methods:
```
   table.columnNames();  			// returns all column names
   List<Column> = table.columns(); // returns all the columns in the table

// removing columns
   table.removeColumns("Foo");			// keep everything but "foo"
   table.retainColumns("Foo", "Bar");  // only keep foo and bar
   table.removeColumnsWithMissingValues();

// adding columns
   table.addColumns(column1, column2, column3);
```

In **Java DataFrame**, column names are case-insensitive. You get the same column if you ask for any of these:
```
  t.column("FOO");
  t.column("foo");
  t.column("foO");
```
remembering column names is enough of a burden without having to remember exactly which characters are capitalized.

### Getting specific column types from a table
Columns can be retrieved from tables by name or position. The simplest method column() returns a object of type Column. This may be good enough, but often you want to get a column of a specific type. For example, you would need to cast the value returned to a NumberColumn to use its values in a scatter plot.
```
  Column nc = table.column("Foo"); // returns the column named 'Foo' if it's in the table.
  // or 
  Column nc = table.column(0);  // returns the first column

  // To work with a StringColumn you can cast the return value
  StringColumn nc = (StringColumn) table.column(0); 
  // Now you can do some numeric stuff with the column nc
```

Table also supports methods that return columns of the desired type directly:
```
   StringColumn nc = table.stringColumn(0); 
   DateColumn dc = table.dateColumn("start date");
```
If you want all the columns of specific type, you can get those as well. The method columnsOfType(aColumnType) returns them as a List, but you still have to cast the results. For example, to format all columns as ints when you print them, you could do this.
```
   table.columnOfType(ColumnType.DOUBLE).forEach(x ->                                               		((DoubleColumn)x).setPrintFormatter(NumberColumnFormatter.ints()));
```
>> **Key point:** You may want a specific kind of column to work with. Either use the standard column() method and cast the result or use one of the type specific methods (like numberColumn()) that handle the cast for you. There are also methods or getting columns of a specific type.

### Working with rows
As with columns, many options exist for working with tables in row-wise fashion. Here are some useful ones:
```
   Table result = table.dropDuplicateRows();
   result = table.dropRowsWithMissingValues();

// drop rows using Selections
   result = table.dropWhere(table.numberColumn(0).isLessThan(100));

// add rows
   table.addRow(43, sourceTable);	// adds row 43 from sourceTable to the receiver

// sampling
   table.sample(200);				// select 200 rows at random from table 
```
You can also perform arbitrary operations on each row in the table. One way is to just iterate over the rows and work with each column individually, using Row::rowNumber() as the index:
```
   for (Row row : table) {
       System.out.println(column1.get(row.rowNumber())); // etc.
   }
```
There are better ways, however. Another approach lets you skip the iteration and just provide a Consumer for each row.
```
// Create a consumer as an object or lambda (show below)
   Consumer<Row> doable = row -> {
       if (row.getRowNumber() < 5) {
           System.out.println("On "
                              + row.getDate("date")
                              + ": "
                              + row.getDouble("approval"));
       }
   };
// apply the lambda
   table.doWithRows(doable);
```
If you need to process more than one row at a time, there are several methods to help.
```
// work with a sliding window of rows
// for example 0, 1, and 2, then 1, 2, and 3. etc.
   table.rollWithRows(consumer, 3);		

// work with a shifting window of rows
// for example rows 0 through 4, then 5 through 9, etc.
   table.stepWithRows(consumer, 5);		
   table.doWithRowPairs(Pairs)	// easy syntax for working with each pair of rows
```
See ``Rows`` for more information and other options.

### Sorting
To sort a table, you can just use the sort() function and give it a column name (or two):
```
   Table sorted = table.sort("foo", "bar", "bam");
```
The above code sorts in ascending order by default. Other options are shown below:
```
  sorted = table.sortDescending("foo");
  sorted = table.sortAscending("bar"); 	// just like sort(), but makes order explicit.

/* sort on foo ascending, then bar descending. Note the minus sign preceding the name of column bar. */
  sorted = table.sort("foo", "-bar");		 
```
See Sorting for more information and other options.

### Filtering tables with selections
Tables also use selections to perform filtering. The basic approach is similar.
```
   Table t = Table.create("test").addColumns(nc1, nc2);
   Table result = t.where(nc1.isGreaterThan(4));
```
Note that the where() method for tables also takes a selection as its argument. The result is a new table like the original, except that it only contains the rows where the value in the nc1 column is > 4.

Combining filters into complex queries
Query filters can be combined using the logical operations and, or, and not. These are implemented on the table class. The not() method takes a single selection as its argument, while and() and or() take a comma separated list of them. The rather contrived code below shows all three logical operators combined.
```
   Table result = t.where(
	   t.and(nc1.isGreaterThan(4),
            t.or(t.not(nc2.isLessThanOrEqualTo(5)),
         		nc2.isEven()));
```
Selecting columns in a query statement
If you don’t need all the columns from the filtered table in the result, you can limit columns as well as rows, using select().where().
```
    Table result = t.select(nc1).where(nc2.isEven());
    The select() method takes a column or array of columns as arguments.
```
## Statistic Function
---------------
### Map functions
Map functions are methods defined on columns that return other new Columns as their result. You’ve already seen one: The column multiply(aNumber) method above is a map function with a scalar argument. To multiple the values in two columns, use multiply(aNumberColumn):
```
   DoubleColumn newColumn = nc1.multiply(nc2);
```
Each value in column nc1 is multiplied by the corresponding value in nc2, rather than by a scalar value in the earlier example.

There are many map functions built-in for the various column types. Here are some examples for StringColumn:

```
    StringColumn s;
    s = aStringColumn.upperCase();
    s = s.replaceFirst("foo", "bar")
    s = s.substring(3, 10);
    s = s.padEnd(4, 'x');				// put 4 x chars at the end of each string

	// this returns the common prefix of each row in two columns
    y = s.commonPrefix(anotherStringColumn);

	// this returns a measure of the similarity (levenshtein distance) between two columns
    nc = s.distance(anotherStringColumn);
```

As you can see, for many String methods that return a new String. StringColumn provides an equivilent map method that returns a new StringColumn. It also includes other helpful methods found in Guava’s String library and in the Apache Commons String library.

>> **Key point:** Every column type has a set of map operations like ``multiply(aNumber)``. For StringColumn, these methods are defined in the ``tech.tablesaw.columns.strings.StringMapFunctions interface``. It includes many methods beyond those shown above. Methods for all column types can all be found in their filter interfaces located in the sub-folders of ``tech.tablesaw.columns (e.g. tech.tablesaw.columns.dates.DateMapFunctions``, which provides date methods like ``plusDays(anInt)``, ``year()``, and ``month()``).

### Reduce (aggregate) functions: Summarizing a column ###
Sometimes you want to derive a singly value that summarizes in some sense the data in a column. Aggregate functions do just that. Each such function scan all the values in a column and returns a single scalar value as a result. All columns support some aggregate functions: min() and max(), for example, plus count(), countUnique(), and countMissing(). Some also support type-specific functions. BooleanColumn, for example, supports all(), which returns true if all of the values in the column are true. The functions any(), and none(), return true if any or none the values in the column are true, respectively. The functions countTrue(), and countFalse() are also available.

NumberColumn has many more aggregate functions. For example, to calculate the standard deviation of the values in a column, you would call:
```
	double stdDev = nc.standardDeviation();
```	
>> **Key point:** NumberColumn supports many aggregation functions, including many of the most useful. Among those available are ```sum, count, mean, median, percentile(n), range, variance, sumOfLogs```, and so on. These are defined in the ```NumericColumn``` class.

When we discuss tables below, we’ll show how to calculate sub-totals in one or more numeric columns by the values in one or more grouping columns.

### Summarizing tables
#### Groups
Tables can be “sliced” for calculating subtotals. The method splitOn(CategoricalColumns) and splitOn(CategoricalColumnNames) both return an object called TableSliceGroup. A TableSlice is, effectively, a window into a backing table. TableSliceGroup is a collection of these windows, each of which looks and feels like its own table.

For the most part, tables are sliced according to the value of a column or columns. For example, if you have a string column called “province”, and another called “status,” there will be a slice for each combination of provence and status in the table.

The usual way to calculate values is to use the summarize() method:
```
   Table summary = table.summarize("sales", mean, sum, min, max).by("province", "status");
```
It’s important to recognize, that the column need not exist when summarize is invoked. Any map function can be used in the by() statement to group on calculated values. A common use case is in handling dates. You can summarize sales by day-of-week, as follows:
```
   Table summary = table.summarize("sales", mean, median)
        .by(table.dateColumn("sales date").dayOfWeek());
```	 
which says “return the mean and median sales by day of week.”

>> **Key point:** Tables are usually split based on columns, but the columns can be calculated on the fly

See the documentation on Summarizing data, and the classes in the aggregate package for more detail.


## Exercise
---------------
### Case 1
What will be the output of the program ?
```

import static tech.tablesaw.aggregate.AggregateFunctions.mean;
import tech.tablesaw.api.DoubleColumn;
import tech.tablesaw.api.StringColumn;
import tech.tablesaw.api.Table;
import tech.tablesaw.columns.Column;
import tech.tablesaw.io.csv.CsvReadOptions;
import static tech.tablesaw.aggregate.AggregateFunctions.*;

public class TestStarter {

    public static void main(String[] args) throws Exception 
    {
        //1. Membuat variable vector binatang
 
        String[] binatang = {"Kucing", "Anjing", "Kelinci", "Burung", "Ular"};
        
		//2. Membuat variable vector tingkatkelucuan        
		double[] tingkatkelucuan = {90.1, 84.3, 99.7, 80.4 , 40.4 };

		//3. Membuat data frame BinatangPeliharaanLucu dari kedua vector di atas
        Table BinatangPeliharaanLucu = Table.create("Binatang Peliharaan")
	          .addColumns(
		                   StringColumn.create("Jenis Binatang", binatang),
		                   DoubleColumn.create("Rating", tingkatkelucuan));
						   
		//4. Menampilkan strukture data frame BinatangPeliharaanLucu        

        System.out.println(BinatangPeliharaanLucu.structure());  
       
	    //5. Menampilkan isi data frame BinatangPeliharaanLucu

        BinatangPeliharaanLucu.setName("Data Tingkat Kelucuan Binatang Peliharaan");
        System.out.println(BinatangPeliharaanLucu.print());

	    //6. Mencari Rerata kolom Rating data frame BinatangPeliharaanLucu

        BinatangPeliharaanLucu.setName("Rerata Kelucuan Binatang Peliharaan");       
        System.out.println(BinatangPeliharaanLucu.summarize("Rating", mean, sum, min, max).apply());
         
    }
}
```
**Output:**

...?.....

### Case 2
Create application using this pseudocode algorithm :
```
//1. Buatlah variable vector fakultas dengan algoritma sebagai berikut :
//fakultas <- ("Bisnis", "D3 Perhotelan", "ICT", "Ilmu Komunikasi", "Seni dan Desain")

//2. Buatlah variable vector jumlah_mahasiswa dengan algoritma sebagai berikut :
//jumlah_mahasiswa <- (260, 28, 284, 465, 735)

//3. Butalah data frame info_mahasiswa dari kedua vector di atas

//4. Tampilkanlah strukture data frame info_mahasiswa        

//5. Menampilkan isi data frame info_mahasiswa

//6. Mencari Rerata kolom Rating data frame info_mahasiswa untuk data mean, sum, min, max
