# Read Data from HBase Table

### Retrieving Results stored in myTable

We are going to fetch the values that are stored in column families i.e "education" and "projects"

``` HBase
Get g = new Get(Bytes.toBytes("row1"));

Results r = table.get(g);

byte [] value = r.getValue(Bytes.toBytes("education"), Bytes.toBytes("col1"));
byte [] value1 = r.getValue(Bytes.toBytes("projects"), Bytes.toBytes("col2"));
```

### Scanning results

Scanning results using scan command. The values that are stored in row1 will be displayed

``` HBase
String valueStr = Bytes.toString(value);

String valueStr1 = Bytes.toString(value1);

System.out.println("GET: "+education: "+valueStr+"projects: "+valueStr1);

Scan s = new Scan();

s.addColumn(Bytes.toBytes("education"), Bytes.toBytes("col1"));
s.addColumn(Bytes.toBytes("projects"), Bytes.toBytes("col2"));

ResultScanner scanner = table.getScanner(s);
```
