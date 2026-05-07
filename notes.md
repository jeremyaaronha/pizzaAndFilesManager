1. Additional Pizza

HTTP/1.1 201 Created
Connection: close
Content-Type: application/json; charset=utf-8
Date: Thu, 07 May 2026 03:56:21 GMT
Server: Kestrel
Location: http://localhost:5055/Pizza/3
Transfer-Encoding: chunked

{
  "id": 3,
  "name": "Jeremy Pizza",
  "isGlutenFree": false
}

2. Additional Function

void GenerateSalesReport(IEnumerable<string> salesFiles, string outputDirectory)
{
    double totalSales = 0;

    string report = "Sales Summary\n";
    report += "----------------------------\n";

    foreach (var file in salesFiles)
    {
        string salesJson = File.ReadAllText(file);

        SalesData? data = JsonConvert.DeserializeObject<SalesData?>(salesJson);

        double fileTotal = data?.Total ?? 0;

        totalSales += fileTotal;

        report += $"{Path.GetFileName(file)}: {fileTotal:C}\n";
    }

    report += $"\nTotal Sales: {totalSales:C}";

    File.WriteAllText(Path.Combine(outputDirectory, "sales-summary.txt"), report);
}

File Result:

Sales Summary
----------------------------
sales.json: $89
sales.json: $89
salestotals.json: $0
sales.json: $99
salestotals.json: $0
sales.json: $1.234
salestotals.json: $0
sales.json: $501
salestotals.json: $0

Total Sales: $2.012