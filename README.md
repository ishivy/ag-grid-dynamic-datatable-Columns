# ag-grid-dynamic-datatable-Column
Dynamically display column data in ag-grid


import React from 'react';
import {AgGridReact} from 'ag-grid-react';
import 'ag-grid-community/dist/styles/ag-theme-alpine.css';
import 'ag-grid-community/dist/styles/ag-grid.css';
import '../../style/datatable.css';

class DataTable extends React.Component {

  constructor(props) {
    super(props);
    this.state = {
      tableData: [{
        "Accounts":{
          "June": {"25": 0,"26":0,"27":0,"28":0,"29":0,"30":0},
          "July":  {"1": 0,"2":0,"3":0,"4":0,"5":0,"6":0,"7": 0,"8":0,"9":0,"10":0,"11":0,"12":0}
        },
        "Loan":{
          "June": {"25": 0,"26":0,"27":0,"28":0,"29":0,"30":0},
          "July":  {"1": 0,"2":0,"3":0,"4":0,"5":0,"6":0,"7": 0,"8":0,"9":0,"10":0,"11":0,"12":0}
        },
        "Total":{
          "June": {"25": 0,"26":0,"27":0,"28":0,"29":0,"30":0},
          "July":  {"1": 0,"2":0,"3":0,"4":0,"5":0,"6":0,"7": 0,"8":0,"9":0,"10":0,"11":0,"12":0}
        },
      }],
    }
  }

  generateColumns = (data) => {
    let columnDef = [{headerName: "Detail Type", field:"detailtype"}];
    let columnDef = [];
    data.map( obj => {
      Object.values(obj).map(detailType=> {
        Object.keys(detailType).map(monthKey=> {
          let mappedColumnChildrens = [];
          Object.keys(detailType[monthKey]).map(dateKey=> {
            let mappedColumnChildern = {
              headerName: dateKey,
              field: dateKey,
            }
            mappedColumnChildrens.push(mappedColumnChildern)
          })
          let mappedColumn = {
            headerName: monthKey,
            field: monthKey,
            children: mappedColumnChildrens
          }
          columnDef.push(mappedColumn);
        })
      })
    })

    columnDef = columnDef.filter((column, index, self) =>
    index === self.findIndex((colAtIndex) => (
      colAtIndex.field === column.field
    ))
    )
    return columnDefs;

  }

  render() {
    let columnsData = this.generateColumns(this.state.tableData);
    return (
      <div className="ag-theme-alpine" style={ {height: '100%', width:'100%'} }>
        <AgGridReact
            columnDefs={columnsData}
        >
        </AgGridReact>
      </div>
    );
  }
}

export default DataTable;

