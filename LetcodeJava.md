## 反转任意整数

```java
public int resver(int x) {
        
    long resu = 0;
        while (x != 0){
            resu = resu * 10 + x % 10;
            x /= 10;
        }
        if(resu > Integer.MAX_VALUE || resu < Integer.MIN_VALUE){
            return 0;
        }else {
            return (int) resu;
        }
    }
```

