---
layout: post
title: Импорт данных в Quantbase
date: 2021-10-01 08:06:52
tags: C#
hidden: true
excerpt_separator: <!--more-->
---

Загрузить и сохранить данные в QuantBase можно следующим скриптом:

<!--more-->

```

using System;
using OpenQuant.API;

public class LoadHistoryQB : Script
{
   [Parameter]
   public string Instrument = "AAPL";
   
   [Parameter]
   public string Provider = "IQFeed";

   public override void Run()
   {
      Instrument instrument = InstrumentManager.Instruments[Instrument];

      // Load 1 minute bars.
      BarSeries barSeries = DataManager.GetHistoricalBars(Provider, instrument, DateTime.Now.Date, DateTime.Now, 60);

      // Save bars.
      foreach (Bar bar in barSeries)
         DataManager.Add(instrument, bar);

      Console.WriteLine("Loaded and added {0} bars", barSeries.Count);
   }
}

```
