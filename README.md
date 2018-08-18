# nodejs-generate-excel
## Create and donwload excel with nodejs (expressjs)

´´´´javascript
const express = require('express')

// XLS Excel 
const XLSX = require('xlsx');

expressApp.get('/datos', (req, res) => {

    var array = [["ELement 1"], ["ELement 2"], ["ELement 3"], ["ELement 4"]];

    var wb = XLSX.utils.book_new();
    wb.Props = {
        Title: "Excel",
        Subject: "Excel",
        Author: "PookDeveloper",
        CreatedDate: new Date()
    };

    wb.SheetNames.push("ExcelSheet");
    var ws = XLSX.utils.aoa_to_sheet(array);
    wb.Sheets["ExcelSheet"] = ws;

    var wbout = XLSX.write(wb, { bookType: 'xlsx', type: 'buffer' });

    /* send to client */
    res.setHeader('Content-Disposition', 'attachment; filename=' + "FileExcel.xlsx");
    res.setHeader("X-File-Name", "FileExcel.xlsx");
    res.setHeader('Content-Type', 'application/vnd.ms-excel; charset=utf-8')
    res.status(200).send(wbout);
});

expressApp.listen(PORT, () => {
    console.log('Example app listening on port ' + PORT);
})












´´´´
