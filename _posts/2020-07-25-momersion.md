---
layout: post
title: Индикатор momersion by Michael Harris
date: 2021-07-25 11:06:52
tags: R
hidden: true
excerpt_separator: <!--more-->
---

Momersion, индикатор, который измеряет процент двух последовательных восходящих
дней в 252-дневном периоде. Это мера, предназначенная для определения степени тенденции
или возврата к среднему значению ряда доходностей.
<!--more-->

<img src="https://raw.githubusercontent.com/Ragve-hub/scribble/gh-pages/images/momersion.png" alt="">

Значения менее 50 указывают на большее возвращение к среднему по сравнению
со значениями более 50, указывающими на тенденцию к тренду.


# Код

```

momersion <- function(R, n, returnLag = 1) {
  momentum <- sign(R * lag(R, returnLag))
  momentum[momentum < 0] <- 0
  momersion <- runSum(momentum, n = n)/n * 100
  colnames(momersion) <- "momersion"
  return(momersion)
}

```

