---
title: "[C#]三個範例告訴你，什麼是where (泛型類型條件約束)"
keywords :
- C#
- 泛型類型條件約束
- generic type constraint
- where
- 泛型
- 條件約束
- generic
- constraint
description : "三個範例告訴你，什麼是where (泛型類型條件約束)"
author : "Sky Chen"
slug: csharp-generic-type-constraint
tags : ["C#","notes"]
categories:
- notes
- C#

date: "2023-03-16"

toc : true
coverSize: partial
coverImage: images/content/notes0007.jpg
thumbnailImage: images/content/notes0007.jpg
---
<!--more-->

# 三個範例告訴你，什麼是where (泛型類型條件約束)
tags: `C#` `notes`

{{< toc >}}

## 什麼是Where (泛型類型條件約束)?
泛型類型條件約束（generic type constraints）是C#語言中一種用於限制泛型型別參數（generic type parameters）的機制。通過條件約束，可以告訴編譯器該泛型型別參數必須滿足什麼條件，這樣就可以在編譯期間對該參數進行類型檢查，避免在運行時出現類型錯誤。

條件約束可以是以下幾種類型：

1. ```where T : class```：T必須是一個引用類型，而不能是值類型（如int、bool等）。

1. ```where T : struct```：T必須是一個值類型。

1. ```where T : new()```：T必須具有公共的無參數構造函數。

1. ```where T : <base class>```：T必須是指定基類（base class）或其派生類。

1. ```where T : <interface>```：T必須實現指定接口（interface）。

泛型類型條件約束可以提高代碼的安全性和可讀性，也可以幫助開發人員更好地利用C#的泛型特性。
 

## 使用時機
使用where關鍵字來指定泛型類型應該滿足的條件約束可以增強代碼的靜態類型檢查，防止不必要的代碼錯誤。通常在以下情況下會使用where：

當你需要對泛型類型進行限制，以確保它只能是特定的類型（如值類型、引用類型、類、結構等）時，可以使用where關鍵字來指定條件約束。

當你需要在泛型類型中使用特定的方法或屬性時，可以使用where關鍵字來指定條件約束，以確保泛型類型支持該方法或屬性。

## 範例
### 1.where T : class
以下範例展示如何何使用泛型類型條件約束來限制泛型類型參數的類型：
```csharp=
public class ExampleClass<T> where T : class
{
    public T ExampleMethod(T param)
    {
        // 參數param必須是一個引用類型
        return param;
    }
}
```
在上面的範例中，```ExampleClass<T>```是一個泛型類型，它使用了```where T : class```的條件約束，表示T必須是一個引用類型。在ExampleMethod方法中，參數param也必須是一個引用類型，因為它的類型參數T需要滿足條件約束。
    
       
### 2.where T : struct
當你定義一個泛型類或方法時，可以使用where關鍵字來指定泛型類型應該滿足的條件約束。以下是一個簡單的範例：
```csharp=
public class Example<T> where T : struct
{
    public T Value { get; set; }
    
    public Example(T value)
    {
        Value = value;
    }
    
    public bool IsPositive()
    {
        return Value > default(T);
    }
}
```
在這個例子中，我們定義了一個名為Example的泛型類。該類有一個名為Value的屬性和一個名為IsPositive的方法。這個泛型類有一個條件約束，即T必須是一個值類型（struct）。

在IsPositive方法中，我們使用了default關鍵字來獲取T類型的預設值，這樣我們就可以比較Value是否大於預設值（對於大多數值類型來說，預設值是0）。

現在我們可以使用Example類型來創建具有不同值類型的對象。例如，我們可以這樣使用：
```csharp=
var example1 = new Example<int>(5);
var example2 = new Example<double>(-2.5);
var example3 = new Example<DateTime>(DateTime.Now);
```
在這個例子中，我們創建了三個Example對象，分別使用了int、double和DateTime類型作為泛型類型參數。由於int和double都是值類型，而DateTime也是一個struct，所以這些對象都符合```Example<T>```泛型類的條件約束。

我們可以使用IsPositive方法來檢查這些對象是否是正數，例如：
```csharp=
Console.WriteLine(example1.IsPositive()); // true
Console.WriteLine(example2.IsPositive()); // false
```
這將輸出true和false，這取決於example1和example2對象的Value屬性是否大於0。


### 3.where T : interface
以下範例展示如何使用泛型類型條件約束來限制泛型類型參數必須實現指定的接口：
```csharp=
public interface IExampleInterface
{
    void ExampleMethod();
}

public class ExampleClass<T> where T : IExampleInterface
{
    public void ExampleMethod(T param)
    {
        // 參數param必須實現IExampleInterface接口
        param.ExampleMethod();
    }
}
```
在上面的範例中，```ExampleClass<T>```是一個泛型類型，它使用了```where T : IExampleInterface```的條件約束，表示T必須實現IExampleInterface接口。在ExampleMethod方法中，參數param必須實現IExampleInterface接口，才能調用ExampleMethod方法中定義的```param.ExampleMethod()```方法。

## 總結
總的來說，where關鍵字在C#泛型中用於指定泛型類型應該滿足的條件約束。它可以用於限制泛型類型必須是特定的類型（如值類型、引用類型、類、結構等），或實現特定的介面或擁有特定的方法或屬性。使用where可以增強代碼的靜態類型檢查，提高代碼的可靠性、可讀性、易於維護性和可重用性，防止不必要的代碼錯誤。

## 參考連結
[微軟官方文件](https://learn.microsoft.com/zh-tw/dotnet/csharp/language-reference/keywords/where-generic-type-constraint)
