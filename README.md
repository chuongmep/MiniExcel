[![NuGet](https://img.shields.io/nuget/v/MiniExcel.svg)](https://www.nuget.org/packages/MiniExcel)  [![](https://img.shields.io/nuget/dt/MiniExcel.svg)](https://www.nuget.org/packages/MiniExcel)  


### Features
- `Avoid large file OOM(out of memoery)` by IEnumerable Lazy `Step By Step getting one row cells` not until all rows read in memory  
e.g:  Comparison of MiniExcel Query and ExcelDataReader/EPPlus/ClosedXml of reading large Xlsx File
![miniexcel_lazy_load](https://user-images.githubusercontent.com/12729184/111034290-e5588a80-844f-11eb-8c84-6fdb6fb8f403.gif)
- Mini (DLL Size Only 20KB) and easy to use.
- Support .NET Standard 2.0/.NET 4.6/.NET 5
- Without any third party library dependencies
- Support dynamic/type mapping query and create by AnonymousType/DapperRows/List/Array/Set/Enumrable/DataTable/Dictionary

### Installation

You can install the package [from NuGet](https://www.nuget.org/packages/MiniExcel)

### Execute a query and map it to a list of dynamic objects without using head

| MiniExcel     | 1     | 
| -------- | -------- | 
| Github     | 2     | 

```C#
using (var stream = File.OpenRead(path))
{
    var rows = stream.Query().ToList();
                
    Assert.Equal("MiniExcel", rows[0].A);
    Assert.Equal(1, rows[0].B);
    Assert.Equal("Github", rows[1].A);
    Assert.Equal(2, rows[1].B);
}
```

### Execute a query with first header row

| Column1 | Column2 | 
| -------- | -------- | 
| MiniExcel     | 1     |  
| Github     | 2     | 


```C#
using (var stream = File.OpenRead(path))
{
    var rows = stream.Query(useHeaderRow:true).ToList();

    Assert.Equal("MiniExcel", rows[0].Column1);
    Assert.Equal(1, rows[0].Column2);
    Assert.Equal("Github", rows[1].Column1);
    Assert.Equal(2, rows[1].Column2);
}
```

### Create Excel Xlsx file by ICollection Anonymous Type/Datatable
```C#
var path = Path.Combine(Path.GetTempPath(), $"{Guid.NewGuid()}.xlsx");
MiniExcel.Create(path, new[] {
    new { Column1 = "MiniExcel", Column2 = 1 },
    new { Column1 = "Github", Column2 = 2}
});
```

Datatable:  
```C#
var path = Path.Combine(Path.GetTempPath(), $"{Guid.NewGuid()}.xlsx");
var table = new DataTable();
{
    table.Columns.Add("Column1", typeof(string));
    table.Columns.Add("Column2", typeof(decimal));
    table.Rows.Add("MiniExcel", 1);
    table.Rows.Add("Github", 2);
}

MiniExcel.Create(path, table);
```

Create File Result : 

| Column1 | Column2 | 
| -------- | -------- | 
| MiniExcel     | 1     |  
| Github     | 2     | 

### SaveAs Stream

```C#
using (var stream = new FileStream(path, FileMode.CreateNew))
{
    stream.SaveAs(values);
}
```

### TODO

Please Check [Issues · todo](https://github.com/shps951023/MiniExcel/labels/todo)

## Release Notes

Please Check [Release Notes](https://github.com/shps951023/MiniExcel/tree/master/docs)