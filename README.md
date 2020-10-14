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
        System.out.print(i-j+" ");
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
