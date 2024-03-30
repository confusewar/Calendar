html:
<template>
  <table style="background-image:url(https://d2w00000md1qseat-dev-ed--c.develop.vf.force.com/resource/1711105363000/Calendar); table-layout: fixed; width: 100%; height: 60px; text-align: center; border: 1px solid black;">    
      <thead>
          <tr>
            <td colspan ="7" style ="text-align: center; color:solid black; font-size: 20px" height="50px" > MARCH--2024 </td>
          </tr>
  <tr style="table-layout: fixed; width: 100%; height: 60px;">    
  <th style="text-align: center;color: rgb(17, 17, 17); border: 1px solid black;background-color: plum; ">Sunday</th>    
  <th style="text-align: center;color: rgb(17, 17, 17); border: 1px solid black;background-color: plum;">Monday</th>    
  <th style="text-align: center;color: rgb(17, 17, 17); border: 1px solid black;background-color: plum;">Tuesday</th>
  <th style="text-align: center;color: rgb(17, 17, 17); border: 1px solid black;background-color: plum;">Wednesday</th>
  <th style="text-align: center;color: rgb(17, 17, 17); border: 1px solid black;background-color: plum;">Thursday</th>
  <th style="text-align: center;color: rgb(17, 17, 17); border: 1px solid black;background-color: plum;">Friday</th>
  <th style="text-align: center;color: rgb(17, 17, 17); border: 1px solid black;background-color: plum;">Saturday</th>
  </tr>    
  </thead>    
  <tbody>    
  <template for:each={rows} for:item="row">    
  <tr style="table-layout: fixed; width: 100%; height: 60px; text-align: center;" key={row.id}>    
 <template for:each={row.cells} for:item="cell">    
  <template if:true={cell.isSunday}>
  <td style="text-align: center; border: 1px solid black; color: red;" key={cell.id}>{cell.value}</td>
  </template>
  <template if:false={cell.isSunday}>
    <template if:true={cell.isMahaShivaratri}>
      <td style="position: relative;text-align: center; border: 1px solid black; background-color: rgb(182, 236, 242);" key={cell.id}>
      <span style="position: absolute;top: 0;left: 0;font-size:10px;text-align: center;">Maha Shivaratri</span>
      {cell.value}
    </td>
    </template>
      <template if:false={cell.isMahaShivaratri}>
        <template if:true={cell.isHoli}>
          <td style="position: relative;text-align: center; border: 1px solid black;background-color: rgb(202, 145, 199);" key={cell.id}>
          <span style="position: absolute;top: 0;left: 0;font-size:10px;text-align: center;">Holi</span>
          {cell.value}
          </td>
        </template>
          <template if:false={cell.isHoli}>
            <template if:true={cell.isGoodFriday}>
              <td style="position: relative;text-align: center; border: 1px solid black; background-color: rgb(214, 239, 186);" key={cell.id}>
              <span style="position: absolute;top: 0;left: 0;font-size:10px;text-align: center;">Good Friday</span>
              {cell.value}
              </td>
            </template>
              <template if:false={cell.isGoodFriday}>
              <td style="text-align: center; border: 1px solid black; color: black;" key={cell.id}>{cell.value}</td>
              </template>
          </template>
    </template>
  </template>
 </template>    
  </tr>    
  </template>    
  </tbody>    
  </table>    
  </template>

JS:
import { LightningElement, track } from 'lwc';
 
export default class Calendar extends LightningElement {
    @track rows = [];
 
    connectedCallback() {
        this.createTable();
    }
 
    createTable() {
        const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
        const numRows = 6;
        const numCols = 7;
        let counter = 1;
 
        for (let i = 0; i < numRows; i++) {
            let rowCells = [];
            for (let j = 0; j < numCols; j++) {
                let isSunday = days[j] === 'Sunday';
                let isMahaShivaratri  = i === 1 && j==5;
                let isHoli  = i === 4 && j==1;
                let isGoodFriday = i === 4 && j == 5;
                let value = '';
 
                if (i === 0 && days[j] === 'Friday') {
                    value = counter++;
                    console.log(i + 'friday');
                } else if (i === 0 && days[j] === 'Saturday') {
                    value = counter++;
                    console.log(i + 'saturday');
                } else if (i === 1) {
                    value = counter++;              
                } else if (i === 2) {
                    value = counter++;
                } else if (i === 3) {
                    value = counter++;
                } else if (i === 4) {
                    value = counter++;
                } else if (i === 5 && j === 0) {
                    value = counter++;
                }
                rowCells.push({ id: j, value: value, isSunday: isSunday,isMahaShivaratri: isMahaShivaratri,isHoli: isHoli,isGoodFriday: isGoodFriday});
            }
            this.rows.push({ id: i, cells: rowCells });
        }
    }
}

}

