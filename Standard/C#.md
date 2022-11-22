# C# 編碼規範

## 命名原則
```
想像下一個接手你程式碼的人是個暴力傾向的重度精神病患者
而且他知道你住在哪。　　—— 《無瑕的程式碼》
```
- 使用有意義的命名，請重視描述性。除了迴圈計數器例外
- 使用駝峰式命名，但開頭小寫
- 盡量不要超過五個單字
- 業界和慣例中有對應縮寫時可以使用縮寫
- 承上，縮寫兩個字母時全大寫，三個字母以上時只第一字大寫

## 命名空間NameSpace

- 基礎類別庫：{組織} . {大類/應用範圍} . {小類/專案名稱}
```
MyStudio.Libs.Basic
MyStudio.Libs.Web.BaseTools
```
- 專案類別庫：{專案名稱} . {子專案/類別/用途}
```
MyProject.Permiss.Proxy
MyProject.Permiss.Repository
```

## 類別Class
使用名詞或名詞片語，不使用任何前綴，須和檔案名稱相同 類別應該要能夠在 25 個字之內做出描述

- 基底類別 (Basic Class)：後綴 Base
```
public class ProductBase （=產品基底類別）
```
- 一般類別 (General Class) 註：抽象類別與一般類別的命名相同
```
public class Product （=產品類別）
```
- 集合類別 (Collection Class)：後綴 Collection
```
public class ProductCollection （=產品集合類別）
```
- 工廠類別 (Factory Class)：後綴 Factory
```
public class ProductFactory （=產品工廠類別）
```
- Help 類別：應以 Help 名稱、Help 性質方式命名
```
public class SystemTimeHelp
```
- 有使用 Partial 的類別：檔名按照類別階層命名
```
public partial class Core 此類別分散到 Album 和 Banner
    internal Public class Album -> 檔名為 Core.Album.cs
    internal Public class Banner -> 檔名為 Core.Banner.cs
```    
- 列舉：大駱駝峰，並後綴 Enum
```
public enum KeywordTypeEnum
```
- 介面：大駱駝峰，前綴 I
```
ICarFactory
```
