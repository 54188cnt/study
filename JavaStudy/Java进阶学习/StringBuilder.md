## 常用方法

- `StringBuilder append(CharSequence s)` 
- `char charAt(int index)` 
- `StringBuilder delete(int start, int end)` 
- `StringBuilder insert(int offset, CharSequence s)` 
- `int length()` 
- `StringBuilder repeat(CharSequence s, int cnt)` 
- `StringBuilder replace(int start, int end, String str)` 
- `StringBuilder reverse()` 
- `void setCharAt(int index, char ch)` 
- `void setLength(int newLength)` 
- `String toString()` 
- `String substring(int start[, int end])` 

## 其他
StringBuilder 不支持多线程，多线程使用 <span style="background:#affad1">StringBuffer</span>

