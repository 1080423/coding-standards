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

## 變數、屬性
公開變數使用大駱駝峰，例如：
```
public string Name { set; get; }
```
私有變數使用小駱駝峰，看專案決定需不需要加上底線當前綴，例如：
```
private int approvalRating
```
常數一律大寫，但建議使用 static readonly 然後使用大駱駝峰。因為前輩的文件表示過使用常數連結 DLL 時如果修改 DLL 的常數再參考但尚未建置時會導致一些神奇的錯誤
```
const double PI = 3.14159;
static readonly double Pi = 3.14159;
```

命名變數時的注意事項：
- 包含邊界的極值優先使用 min 與 max
- 閉區間優先使用 first 與 end
- 半開放區間優先使用 begin 與 end
- Boolean 變數開頭必須使用 is can has should 或有狀態差異的形容詞

宣告變數時的注意事項：
- 變數越多越難記得所有變數
-- 減少沒用到的、或對可讀性沒有幫助的變數
變數存活的範圍越大，就必須記越久
盡量避免使用全域變數，縮限並控制所有變數的範圍
變數越常改變越難記得目前的數值和意義
偏好單次寫入變數，盡量不要過度重複寫入造成混亂
當變數內容改變，就可以考慮宣告成新的變數
變數的宣告和其命名都是為了讓閱讀者能直接看出改變的差異或當下變數的狀態
