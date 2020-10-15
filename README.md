# String Pattern Search hands-on

### KMP Algorithm
```
import java.util.*;

public class PatternMatch{

  public static void fillLPS(String str, int lps[]){
    int len = 0;
    lps[0] = len;
    int i = 1;
    int n = str.length();
    while(i<n){
      if(str.charAt(i)==str.charAt(len)){
        lps[i++]=++len;
      } else {
        if(len==0){
          lps[i]=0;
          i++;
        } else {
          len = lps[len-1];
        }
      }
    }
  }
  
  public static void KMP(String pat, String txt){
    int n = txt.length();
    int m = pat.length();
    int lps[] = new int[m];
    fillLPS(pat,lps);
    int i=0,j=0;
    while(i<n){
      if(pat.charAt(j)==txt.charAt(i)){
        i++;
        j++;
      }
      if(j==m){
        System.out.print(i-m+" ");
        j = lps[j-1];
      } else if(i<n && pat.charAt(j)!=txt.charAt(i)) {
        if(j==0){
          i++;
        } else {
          j = lps[j-1];
        }
      }
    }
  }
}
```

### Rabin-Karp Algorithm

```
import java.util.*;

public class PatternMatch{

  public final static int d = 256;
  public static void RKSearch(String pat, String txt, int q){
    int n = txt.length();
    int m = pat.length();
    
    int h = 1;
    for(int i=1;i<=m-1;i++){
      h = (h*d)%q;
    }
    
    int p=0,t=0;
    for(int i=0;i<m;i++){
      p = (d*p + pat.charAt(i))%q;
      t = (d*t + txt.charAt(i))%q;
    }
    
    for(int i=0;i<=n-m;i++){
      if(p==t){
        int j = 0;
        for(j=0;j<m;j++){
          if(txt.charAt(i+j)!=pat.charAt(j)){
            break;
          }
        }
        if(j==m){
          System.out.print(i+ " ");
        }
      }
      
      if(i<n-m){
        t = (d*(t - txt.charAt(i)*h) + txt.charAt(i+m))%q;
        if(t<0)
          t=t+q;
      }
    }
  }
}
```

### Distinct Pattern Naive Algorithm
```
import java.util.*;

public class PatternMatch{

  public static void naiveSearch(String pat, String txt){
    int n = txt.length();
    int m = pat.length();
    for(int i=0;i<=n-m;){
        int j;
        for(j=0;j<m;j++){
            if(txt.charAt(i+j)!=pat.charAt(j)){
                break;
            }
        }
        if(j==m){
            System.out.print(i + " ");
        }
        if(j==0){
            i++;
        } else {
            i+=j;
        }
    }
  }
}
```
