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
}
```
