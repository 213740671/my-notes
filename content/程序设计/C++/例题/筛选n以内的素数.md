# 题目
![[Pasted image 20260119113620.png]]

# 代码
```cpp
//输入nn列出0-nn的所有素数  
#include<bits/stdc++.h>  
using namespace std;  
  
int main(){  
    int nn;  
    cin>>nn;  
    for (int i=2;i<=nn;i++) {  
        int flag=0;  
        for (int j=2;j<=pow(i,0.5);j++) {  
            if (i%j==0) {  
                flag=1;  
                break;  
            }  
        }  
        if (flag==0) {  
            cout<<i<<endl;  
        }  
    }  
    return 0;  
}
```
# 知识点
[[素数的边界判断]]
>[!note]+ 开方的判断
>既可以写成pow(i,0.5)
> 也可以写成j * j<=i

