
<script >
import { DropDownTreeComponent } from "@syncfusion/ej2-vue-dropdowns";
import { DataManager,Query,ODataV4Adaptor } from "@syncfusion/ej2-data";
var remoteData = new DataManager({
    url: 'https://services.odata.org/V4/Northwind/Northwind.svc',
            adaptor: new ODataV4Adaptor,
            crossDomain: true,
});
var dataQuery = new Query().from('Employees').select('EmployeeID,FirstName,Title').take(5);
var childDataQuery = new Query().from('Orders').select('OrderID,EmployeeID,ShipName').take(5);
var LocalData =  [
 { id: '01', name: 'Local Disk (C:)', expanded : true,
    subChild: [
     { id: '01-01', name: 'Program Files', expanded : true,
     subChild: [
       { id: '01-01-01', name: '7-Zip' },
       { id: '01-01-02', name: 'Git' },
       { id: '01-01-03', name: 'IIS Express' }
     ]
     },
     { id: '01-02', name: 'Users', expanded : true,
     subChild: [
       { id: '01-02-01', name: 'Smith' },
       { id: '01-02-02', name: 'Admin' }
      ]
     },
     { id: '01-03', name: 'Windows',
     subChild: [
       { id: '01-03-01', name: 'FileManager' } 
      ]
     }
    ]
 },
 { id: '02', name: 'Local Disk (D:)',
    subChild: [
     { id: '02-01', name: 'Personals' },
     { id: '02-02', name: 'Projects' }
   ]
 },
 { id: '03', name: 'Local Disk (E:)',
    subChild: [
     { id: '03-01', name: 'Pictures' }, 
     { id: '03-02', name: 'Documents' } 
   ]
 }


   ];
export default {
    components: {
        'ejs-dropdowntree': DropDownTreeComponent
    },
    data (){
    return {
      fields: { dataSource: LocalData, value: 'id', text: 'name', child: 'subChild'},
      remoteDataFields: { dataSource: remoteData, query:dataQuery, value: 'EmployeeID', text: 'FirstName', hasChildren: 'EmployeeID',
      child: { dataSource: remoteData, query:childDataQuery, value: 'OrderID', parentValue: 'EmployeeID', text: 'ShipName' }},
      treeSettings:{autoCheck:true}
    }
  }
    }


   
</script>
<template>
 <ejs-dropdowntree :fields='remoteDataFields' placeholder="Select a folder" popupHeight='200px' 
 allowMultiSelection='true' showCheckBox='true' :treeSettings='treeSettings'
 
 ></ejs-dropdowntree>
 
</template>
<style>
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
@import "../node_modules/@syncfusion/ej2-navigations/styles/material.css";
@import "../node_modules/@syncfusion/ej2-vue-dropdowns/styles/material.css";
</style>