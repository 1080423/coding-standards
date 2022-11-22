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
**使用名詞或名詞片語，不使用任何前綴，須和檔案名稱相同 類別應該要能夠在 25 個字之內做出描述**

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
**公開變數使用大駱駝峰，例如：**
```
public string Name { set; get; }
```
**私有變數使用小駱駝峰，看專案決定需不需要加上底線當前綴，例如：**
```
private int approvalRating
```
**常數一律大寫，但建議使用 static readonly 然後使用大駱駝峰。因為前輩的文件表示過使用常數連結 DLL 時如果修改 DLL 的常數再參考但尚未建置時會導致一些神奇的錯誤**
```
const double PI = 3.14159;
static readonly double Pi = 3.14159;
```

**命名變數時的注意事項：**
* 包含邊界的極值優先使用 min 與 max
* 閉區間優先使用 first 與 end
* 半開放區間優先使用 begin 與 end
* Boolean 變數開頭必須使用 is can has should 或有狀態差異的形容詞

**宣告變數時的注意事項：**
* 變數越多越難記得所有變數
    * 減少沒用到的、或對可讀性沒有幫助的變數
* 變數存活的範圍越大，就必須記越久
    * 盡量避免使用全域變數，縮限並控制所有變數的範圍
* 變數越常改變越難記得目前的數值和意義
    * 偏好單次寫入變數，盡量不要過度重複寫入造成混亂
    * 當變數內容改變，就可以考慮宣告成新的變數
    * 變數的宣告和其命名都是為了讓閱讀者能直接看出改變的差異或當下變數的狀態

## 方法
**一律使用大駱駝峰，前綴字規定如下**
* 擷取
    * Get：從資料庫抓回資料
    * Search：頁面或定義為搜尋時
    * Find：在既有的資料集合找資料
    * Fetch：從遠端 (透過API) 獲取資料，例如：`FetchUsers()
    * load：從本地端加載資料，例如：LoadFile()
* 修改
    * Update：對資料庫的異動
    * Modify：現有變數或資料集合的變動
* 建立
    * Insert：資料庫的資料建立
    * Create：資料集合或物件的建立
    * Generate：單純產生特定資料供使用
* 刪除
    * Delete：資料庫的資料刪除（資料將不存在）
    * Remove：資料集合的資料移除／資料間的關係移除（資料仍存在）
* 其他
    * Convert：代碼轉文字／編碼之間的轉換
    * calculate/calc：通過計算獲取資料，例如：CalcBMI()
    * show：顯示物件，例如：ShowDialog()
    * on：定義 event 的時候使用，像是 OnClick(), OnChange()
    * handle：當 OnClick 之類的 event 發生時所觸發的 function

方法中用到的參數視作私有變數，使用小駱駝峰，如：
```
(string name, int age)
```
如果有泛型直接使用 T 做表示，如：
```
（ List<T> T1, List<T> T2）
```

## 其他注意事項
* 比起弄很多大櫃子然後把東西都塞進去，分工明確的小抽屜更方便靈活
* 輸入參數應該越少越好，如果參數高於三個以上，試著換個思路重構這個方法
* 輸入參數不要使用傳入 Boolean 來改變類別和函式的行為（違反單一職責）
* 有多載的需求時，將輸入參數最多的宣告設為 virtual，其他較少輸入參數的則以呼叫最多輸入參數的函式來完成建構
* 如果類別的名稱已經有足夠的說明，則方法名稱就不需要再複誦一次
    * 例如 ProductService.GetProduct() 就是贅詞
    * 可以改為 ProductService.Get() 就好
* 呼叫方法時，如果傳入參數無法直接識別內容，則應使用具名傳遞
    * 例如 Get(productId, true) 很難看出來 true 代表的意思
    * 可以改為 Get(productId, isInStock: true) 就好
* 回傳值除了單純的運算式以外，一律回傳變數
* 參考資料
[EngTW/English-for-Programmers: 《程式英文》：用英文提昇程式可讀性 (github.com)](https://github.com/EngTW/English-for-Programmers)

[已核准的 PowerShell 命令動詞 - PowerShell | Microsoft Docs](https://docs.microsoft.com/zh-tw/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7.2#common-verbs)

# 斷行與縮排
```
整潔的程式碼讀起來就像一篇優美的散文

　　—— 《無瑕的程式碼》
```

* 不要過多的斷行，也不要都擠在一起，組織成不同的段落
    * 方法之間空一行
    * 參數過長時斷至下一行
    * 程式碼單行欄位數目以不超過 100~120 字元為原則
* 不要省略括弧，讓程式碼範疇／區塊明顯可見
    * 迴圈和 IF 等區塊確實斷行和使用括弧，以維持可閱讀性
    * 運算式的優先部分也要加上括弧，方便一眼看出計算順序
* 使 code 的順序流暢
    * 參數按照傳入的順序排列
    * 相似方法之間的傳入參數順序盡可能一致
    * 相關的宣告和操作放在一起
* 當因為參數過多的時候必須斷到下一行時，從第一個參數之前就開始斷行
    * 因本條規則斷行後，則一個參數獨立一行，必要時具名，使閱讀時能直接往下閱讀
    * 不過如果方法參數過多，應先考慮是否重構該方法，極可能違反單一職責
* 風格一致、風格一致、風格一致
```
風格一致很重要，所以說三次
風格一致很重要，所以說三次
風格一致很重要，所以說三次
```

# 邏輯運算
* 儘管區塊只有一行（例如 if else），仍一律使用大括號，避免改寫時沒注意到
* 條件式的左側為「變化值」、右側則是前者的「比較基準」
    * 符合口語邏輯：如果你高於 180 公分 => if(lenght > 180)
* 處理 if/else 的順序時，大多有以下思路
    * 先處理肯定的再處理否定的（如：if 成功 else 失敗）
    * 先處理簡單的再處理複雜的（如：if 按下傳送前已驗證 else 各種雜七雜八的驗證）
    * 先處理比較有趣或明顯的（如： if 管理者 else 其他使用者）

# 三元運算式
簡單卻繁瑣的時候使用，若複雜的時候，請務必使用if else。例如：
```
//good
string gender = (member.Sex == "F") ? "女性" : "男性"; 

//bad
int result = (exponent >= 0)? mantissa * (1 << exponent): mantissa / (1 << -exponent)
```

# 迴圈
- **迴圈不要用 do/while**
    * 除非你有逼不得已的苦衷...
    * 因為大多數方法和區塊邏輯判斷都在前面，因此使用後置條件會影響閱讀性
- **減少巢狀結構，不要玩波動拳**
    * 減少巢狀的有效方法是「儘早返回」：直接離開當前的函式
    * 迴圈中可以使用 continue 或 break 來直接進入下一個或離開
    * 在方法／函式中可以先處理能直接 return 結果離開的區塊
    * 發生錯誤或非預期結果時可以直接擲出錯誤 throw new Exception 中斷程式

# 存取修飾詞
型別的存取層級，用來控制其他程式碼能不能使用這些型別或內容成員，也就是指定能夠存取的範圍，進而避免誤用、亂用或其他錯誤。
* Public
    * 可以讓同組件和參考該組件的任何其他程式碼存取
* Private
    * 只能由相同類別或結構中的程式碼存取
* Protected
    * 只能由相同類別或結構，或是從該類別衍生的類別存取
* Internal / Friend
    * 可由相同組件的任何程式碼存取，但是其他組件的程式碼不能存取
* Static / Shared
    * 用來宣告靜態成員
    * 此成員屬於型別本身而不屬於任何物件（＝全實體共用同個成員）
    * 不能用在索引子 (Indexer)、解構函式 (Destructor) 以及不在類別裡的型別

# 註解
基本上對各個格式（如結構、函數）都必須加上說明註解，其中的參數和成員（例如列舉）也必須說明。 
Visual Studio 中 /// 就會幫忙把參數註解格式打好。例如：
```
/// <summary>
/// 資料庫連線類別
/// </summary>
public class DatabaseConstants : IDatabaseConstants
{
    // Something
}
```

* 註解重點在於：
    * 簡短敘述，避免模稜兩可或不知去向的代名詞（例如：更新那個物件）
    * 描述函式行為，例如（計算檔案的行數 => 計算檔案中的換行位元個數(\n)）
    * 描述處理過程的原因，要知道做了什麼可以直接看程式碼，要知道為什麼做只能看註解
    * 常數旁邊一定要做原因或用途的說明
    * 函式可以加上範例 <example> Strip("aba","ab") return "a" </example>
    * 移除不需要的註解，例如日誌、署名、重複資訊、被註解掉的 code 之類
    * 使用註解標籤：Todo = 待辦事項； Fixme = 需修復；可搭配 VS 內建的工作清單

# 型別
## 實質型別
    包含所有的數字型別、布林、字元和日期，以及結構和列舉
* 傳值
* 不允許 Null （除非特別指派 Nullable）
* 有隱含的預設建構式，不需要用 new
* 初始化之後才能使用
* 資料傳遞時是將資料複製到另一個變數

## 參考型別
能進一步分為陣列和類別型別，其中包含字串、所有陣列、類別、委派和介面。以及匿名和通用型別
* 傳址
* 必須要使用 new 建立實體，並將該實體的參考記在變數
* 資料傳遞時是將參考複製到另一個變數
```
註記：字串比較特別，實際上比較像一個結構。可以試著當成字元的串列比較好記，
可以從 char[] letters = {'H','e','l','l','o'}; 和 string a = new string(letters); 的實驗中感覺到一絲端倪。
字串建立後也不允許直接變更，可能是藉此閃避一些更改時的問題。
這牽扯到較底層的語言邏輯與規則，我們之後有機會再說
```
## 轉型
* 隱含轉換
    * 屬於安全的轉換，所以不用使用特殊語法
    * 小型到大型整數型別的轉換（如 int -> long）
    * 衍生型別 (Derived Class) 到基底型別 (Base Class) 的轉換
    * 例如 int num = 2147483647; long bigNum = num;
* 明確轉換
    * 資料可能在轉換中遺失或失敗時，需要使用轉型運算子
    * 往精確度較低或範圍較小的型別進行的數值轉換（如 double -> int）
    * 基底類別往衍生類別的轉換
    * 例如 double x = 1234.7; int y= (int)x
* 使用 Helper 類別轉換
    * 在不相容型別間進行轉換時使用（如 int -> System.DateTime）
    * 使用 Helper 進行轉換（如 Int32.Parse），例如
    * System.BitConverter 類別
    * System.Convert 類別
    * 內建數字型別 (Numeric Type) 的 Parse 方法
    * 例如 string x = "2016-04-08"; DateTime z = System.DateTime.Parse(x)

