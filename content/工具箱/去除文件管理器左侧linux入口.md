

1. `Win + R` → 输入 `regedit`
    
2. 找到：  
    `HKEY_CURRENT_USER\Software\Classes\CLSID`
    
3. 新建项：`{B2B4A4D1-2754-4140-A2EB-9A76D9D7CDC6}`
    
4. 在该项下新建 DWORD（32位）：`System.IsPinnedToNameSpaceTree`
    
5. 值设为：`0`
    
6. 重启资源管理器/电脑
    

同样来源于相同的官方/社区教程思路。