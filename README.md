# How to perform sorting in Syncfusion Flutter DataTable

The Syncfusion Flutter DataTable widget provides the support to sort one or more columns in ascending or descending order. You can enable sorting by setting the allowSorting property to true.

When allowSorting is true, you can sort the data simply by tapping column header cell. Once sorting is applied, the datagrid shows a sort icon in the corresponding column header to indicate the sort direction.

The following steps explains how to apply sorting in Syncfusion Flutter DataTable:

## STEP 1
First, create a data source class by extends DataGridSource for mapping data to the SfDataGrid.

```xml
class EmployeeDataSource extends DataGridSource {
  EmployeeDataSource({required List<Employee> employees}) {
    _employeeData = employees
        .map<DataGridRow>((e) => DataGridRow(cells: [
              DataGridCell<int>(columnName: 'id', value: e.id),
              DataGridCell<String>(columnName: 'name', value: e.name),
              DataGridCell<String>(columnName: 'city', value: e.city),
              DataGridCell<int>(columnName: 'freight', value: e.freight),
            ]))
        .toList();
  }
 
  List<DataGridRow> _employeeData = [];
 
  @override
  List<DataGridRow> get rows => _employeeData;
 
  @override
  DataGridRowAdapter? buildRow(DataGridRow row) {
    return DataGridRowAdapter(
        cells: row.getCells().map<Widget>((e) {
      return Container(
        alignment: ['id', 'freight'].contains(e.columnName)
            ? Alignment.centerRight
            : Alignment.centerLeft,
        padding: const EdgeInsets.symmetric(horizontal: 16.0),
        child: Text(e.value.toString()),
      );
    }).toList());
  }
}
```
## STEP 2

Initialize the SfDataGrid widget with all the required properties and set allowSorting property to true.

```xml
class MyHomePage extends StatefulWidget {
  MyHomePage({Key? key}) : super(key: key);
 
  @override
  _MyHomePageState createState() => _MyHomePageState();
}
 
class _MyHomePageState extends State<MyHomePage> {
  late EmployeeDataSource _employeeDataSource;
 
  @override
  void initState() {
    super.initState();
    _employeeDataSource = EmployeeDataSource(employees: populateData());
  }
 
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Syncfusion Flutter DataGrid'),
      ),
      body: SfDataGrid(
        source: _employeeDataSource,
        allowSorting: true,
        columns: <GridColumn>[
          GridTextColumn(
              columnName: 'id',
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerRight,
                  child: Text(
                    'ID',
                  ))),
          GridTextColumn(
              columnName: 'name',
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerLeft,
                  child: Text(
                    'Name',
                  ))),
          GridTextColumn(
              columnName: 'city',
              width: 110,
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerLeft,
                  child: Text(
                    'City',
                    overflow: TextOverflow.ellipsis,
                  ))),
          GridTextColumn(
              columnName: 'Freight',
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerRight,
                  child: Text('Freight'))),
        ],
      ),
    );
  }
 
  List<Employee> populateData() {
    return <Employee>[
      Employee(10001, 'James', 'Bruxelles', 20000),
      Employee(10002, 'Kathryn', 'Rosario', 30000),
      Employee(10003, 'Lara', 'Recife', 15000),
      Employee(10004, 'Michael', 'Graz', 15000),
      Employee(10005, 'Martin', 'Montreal', 15000),
      Employee(10006, 'Newberry', 'Tsawassen', 15000),
      Employee(10007, 'Balnc', 'Campinas', 15000),
      Employee(10008, 'Perry', 'Resende', 15000),
      Employee(10009, 'Gable', 'Resende', 15000),
      Employee(10010, 'Grimes', 'Recife', 15000),
      Employee(10011, 'Newberry', 'Tsawassen', 15000),
      Employee(10012, 'Balnc', 'Campinas', 15000),
      Employee(10013, 'Perry', 'Resende', 15000),
      Employee(10014, 'Gable', 'Resende', 15000),
      Employee(10015, 'Grimes', 'Recife', 15000),
    ];
  }
}
```

## Multi-column sorting 

You can sort the multiple columns by setting the allowMultiColumnSorting property to true. Once multi sorting is applied, you can sort multiple columns by tapping desired column headers. If you want to apply multi sorting in web, you can simply click the column header by pressing the Ctrl key.

```xml
 @override
  Widget build(BuildContext context) {
    return SfDataGrid(
        allowSorting: true,
        allowMultiColumnSorting: true,
        source: _employeeDataSource,
        columns: <GridColumn>[
          GridTextColumn(
              columnName: 'id',
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerRight,
                  child: Text(
                    'ID',
                  ))),
          GridTextColumn(
              columnName: 'name',
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerLeft,
                  child: Text(
                    'Name',
                  ))),
          GridTextColumn(
              columnName: 'city',
              width: 110,
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerLeft,
                  child: Text(
                    'City',
                    overflow: TextOverflow.ellipsis,
                  ))),
          GridTextColumn(
              columnName: 'Freight',
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerRight,
                  child: Text('Freight'))),
    ]);
  }
```

Additionally, you can display the sequence numbers to identify the order of sorted columns during multi-column sorting by setting showSortNumbers property to true.

```xml
  @override
  Widget build(BuildContext context) {
    return SfDataGrid(
        allowSorting: true,
        allowMultiColumnSorting: true,
        showSortNumbers: true,
        source: _employeeDataSource,
        columns: <GridColumn>[
          GridTextColumn(
              columnName: 'id',
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerRight,
                  child: Text(
                    'ID',
                  ))),
          GridTextColumn(
              columnName: 'name',
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerLeft,
                  child: Text(
                    'Name',
                  ))),
          GridTextColumn(
              columnName: 'city',
              width: 110,
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerLeft,
                  child: Text(
                    'City',
                    overflow: TextOverflow.ellipsis,
                  ))),
          GridTextColumn(
              columnName: 'Freight',
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerRight,
                  child: Text('Freight'))),
    ]);
  }
```
## Tri-state sorting

You can unsort the data to its original order by clicking the column header again after sorting to descending order. This can be done by setting the allowTriStateSorting property to true.


```xml
 @override
  Widget build(BuildContext context) {
    return SfDataGrid(
        allowSorting: true,
        allowTriStateSorting: true,
        source: _employeeDataSource,
        columns: <GridColumn>[
          GridTextColumn(
              columnName: 'id',
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerRight,
                  child: Text(
                    'ID',
                  ))),
          GridTextColumn(
              columnName: 'name',
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerLeft,
                  child: Text(
                    'Name',
                  ))),
          GridTextColumn(
              columnName: 'city',
              width: 110,
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerLeft,
                  child: Text(
                    'City',
                    overflow: TextOverflow.ellipsis,
                  ))),
          GridTextColumn(
              columnName: 'Freight',
              label: Container(
                  padding: const EdgeInsets.symmetric(horizontal: 16.0),
                  alignment: Alignment.centerRight,
                  child: Text('Freight'))),
    ]);
  }
```

**[View document in Syncfusion Flutter Knowledge base](https://www.syncfusion.com/kb/12217/how-to-perform-sorting-in-flutter-datatable-sfdatagrid)**