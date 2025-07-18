---
title:  "Импорт данных из csv файла"
date:   2021-12-20
tags: [C#]
---


Несколько вариантов импорта внешних данных из файла csv на примере сценария


1)

```c#

using System;
using System.IO;

using OpenQuant.API;

public class MyScript : Script
{
   public override void Run()
   {
      const string dataDir = @"D:\Data\CSV\";

      long dailyBarSize = 86400;
      
      string[] filenames = new string[]
         {
            "AAPL.csv",
            "CSCO.csv",
            "MSFT.csv"
         };

      // CSV data files have invariant date/number format
      System.Globalization.CultureInfo culture = System.Globalization.CultureInfo.InvariantCulture;
      
      foreach (string filename in filenames)
      {
         Console.WriteLine();
         
         string path = dataDir + filename;

         // check file exists
         if (!File.Exists(path))
         {
            Console.WriteLine(string.Format("File {0} does not exists.", path));
            
            continue;
         }
         
         Console.WriteLine(string.Format("Processing file {0} ...", path));
         
         // get instrument
         string symbol = filename.Substring(0, filename.IndexOf('.'));

         Instrument instrument = InstrumentManager.Instruments[symbol];
         
         if (instrument == null)
         {
            Console.WriteLine(string.Format("Instrument {0} does not exist.", symbol));
            
            continue;
         }
         
         // read file and parse data
         StreamReader reader = new StreamReader(path);
         
         reader.ReadLine(); // skip CSV header
         
         string line = null;
         
         while ((line = reader.ReadLine()) != null)
         {
            string[] items = line.Split(',');

            // parse data
            DateTime date = DateTime.ParseExact(items[0], "yyyy-M-d", culture);

            double high  = double.Parse(items[1], culture);
            double low   = double.Parse(items[2], culture);
            double open  = double.Parse(items[3], culture);
            double close = double.Parse(items[4], culture);
            
            long volume  = long.Parse(items[5], culture);

            // add daily bar
            DataManager.Add(
               instrument,
               date,
               open,
               high,
               low,
               close,
               volume,
               dailyBarSize);
         }
         
         reader.Close();
         
         //
         Console.WriteLine(string.Format("CSV data for {0} was successfully imported.", instrument.Symbol));
      }
   }
}


```
2)

```C#

using System;
using System.IO;

using OpenQuant.API;

public class MyScript : Script
{
   public override void Run()
   {
      const string dataDir = @"C:\ua\Files\OQ_Import\";

      long dailyBarSize = 86400;
         
      //Lookup Directory & File Info
      DirectoryInfo directory_Info = new DirectoryInfo(@"C:\ua\Files\OQ_Import\");
      FileInfo[] file_Info = directory_Info.GetFiles("*.csv");
      
      // CSV data files have invariant date/number format
      System.Globalization.CultureInfo culture = System.Globalization.CultureInfo.InvariantCulture;
      
      foreach (FileInfo file_info in file_Info)
      {
         Console.WriteLine(file_info.Name.Substring(0, file_info.Name.IndexOf('.')));
                  
         Console.WriteLine();
         
         string filename = file_info.Name.Substring(0, file_info.Name.IndexOf('.'));
         string path = dataDir + filename + ".csv";
                  
         // check if file exists
         if (!File.Exists(path))
         {
            Console.WriteLine(string.Format("File {0} does not exists.", path));
           
            continue;
         }
         
         Console.WriteLine(string.Format("Processing file {0} ...", path));
         
         // get instrument
         string symbol = filename; //.Substring(0, filename.IndexOf('.'));

         Instrument instrument = InstrumentManager.Instruments[symbol];
         
         if (instrument == null)
         {
            Console.WriteLine(string.Format("Instrument {0} does not exist.", symbol));
           
            continue;
         }
         
         // read file and parse data
         StreamReader reader = new StreamReader(path);
         
         reader.ReadLine(); // skip CSV header
         
         string line = null;
         
         while ((line = reader.ReadLine()) != null)
         {
            string[] items = line.Split(',');

            // parse data
            DateTime date = DateTime.ParseExact(items[0], "yyyyMMdd", culture);

            double open  = double.Parse(items[3], culture);
            double high  = double.Parse(items[4], culture);
            double low   = double.Parse(items[5], culture);
            double close = double.Parse(items[6], culture);
            long volume  = long.Parse(items[7], culture);
            
            // add daily bar
            DataManager.Add(
               instrument,
               date,
               open,
               high,
               low,
               close,
               volume,
               dailyBarSize);
         }
         
         reader.Close();
         
         //
         Console.WriteLine(string.Format("CSV data for {0} was successfully imported.", instrument.Symbol));
      }
   }
}

```
