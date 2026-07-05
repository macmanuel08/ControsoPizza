## Additional record response / POST Request

HTTP/1.1 201 Created
Connection: close
Content-Type: application/json; charset=utf-8
Date: Sun, 05 Jul 2026 06:10:09 GMT
Server: Kestrel
Location: http://localhost:5039/Pizza/3
Transfer-Encoding: chunked

{
  "id": 3,
  "name": "Pepperoni",
  "isGlutenFree": false
}

## GET
HTTP/1.1 200 OK
Connection: close
Content-Type: application/json; charset=utf-8
Date: Sun, 05 Jul 2026 06:14:14 GMT
Server: Kestrel
Transfer-Encoding: chunked

[
  {
    "id": 1,
    "name": "Classic Italian",
    "isGlutenFree": false
  },
  {
    "id": 2,
    "name": "Veggie",
    "isGlutenFree": true
  },
  {
    "id": 3,
    "name": "Pepperoni",
    "isGlutenFree": false
  }
]

## PUT

HTTP/1.1 204 No Content
Connection: close
Date: Sun, 05 Jul 2026 06:16:25 GMT
Server: Kestrel

## DELETE

HTTP/1.1 204 No Content
Connection: close
Date: Sun, 05 Jul 2026 06:17:10 GMT
Server: Kestrel

## Aditional Function
```C#
IEnumerable<string> FindFiles(string folderName)
{
    List<string> salesFiles = new List<string>();

    var foundFiles = Directory.EnumerateFiles(folderName, "*", SearchOption.AllDirectories);

    foreach (var file in foundFiles)
    {
        // if (file.EndsWith("sales.json"))
        // {
        //     salesFiles.Add(file);
        // }

        var extension = Path.GetExtension(file);
        if (extension == ".json")
        {
            salesFiles.Add(file);
        }
    }

    return salesFiles;
}

void SummarySales()
{
    double salesTotal = 0;

    var currentDirectory = Directory.GetCurrentDirectory();
    var storesDirectory = Path.Combine(currentDirectory, "stores");

    var salesTotalDir = Path.Combine(currentDirectory, "salesTotalDir");
    Directory.CreateDirectory(salesTotalDir);

    var salesFiles = FindFiles(storesDirectory);

    File.AppendAllText(Path.Combine(salesTotalDir, "totalsSummary.txt"), $"Sales Summary{Environment.NewLine}");
    File.AppendAllText(Path.Combine(salesTotalDir, "totalsSummary.txt"), $"\tDetails:{Environment.NewLine}");

    foreach (var file in salesFiles)
    {      
        string salesJson = File.ReadAllText(file);

        SalesData? data = JsonConvert.DeserializeObject<SalesData?>(salesJson);

        File.AppendAllText(Path.Combine(salesTotalDir, "totalsSummary.txt"), $"\t{file}: ${data?.Total ?? 0}{Environment.NewLine}");
        salesTotal += data?.Total ?? 0;
    }

    File.AppendAllText(Path.Combine(salesTotalDir, "totalsSummary.txt"), $"{Environment.NewLine}----------------------------{Environment.NewLine}");
    File.AppendAllText(Path.Combine(salesTotalDir, "totalsSummary.txt"), $"\tTotal Sales: ${salesTotal}");
}

```
