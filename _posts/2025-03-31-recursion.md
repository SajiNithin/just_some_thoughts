

```PHP
<?php
$array = [1,2,3,4,5,6];
function recurse($a,$sum_= 0 ){
    
    if(empty($a)){
        // echo $sum_;
        return array('val'=>$sum_);
    }
    $sum_ =$sum_ + array_shift($a);
    
    recurse($a,$sum_);
    
}
$val = recurse($array);
print_r($val) ;
?>
```
When I first wrote this function, I expected it to simply return the sum. However, it didn’t, which left me confused. Strangely, when I printed (or echoed) the variable, it displayed the correct value. This meant that the core logic of my function wasn’t flawed.

The real confusion began when I checked the return value’s type and saw that it was null. But how? I had explicitly coded the function to return the sum!

After about thirty minutes of debugging, I finally discovered the issue. The function was indeed returning the correct sum—but only in the last recursive call. The problem was that after the final recursive function returned the sum, the earlier recursive calls didn’t return anything. Many of them never reached the condition where a value was returned, so they ended up returning null by default.

As a result, the function I initially called (the base function) wasn’t returning the sum—it was returning null instead. The correct return value was essentially lost amidst all these null returns.
<pre class="mermaid">
graph TD;
    A["returns 21"] --> B["return null"];
    B --> C["return null"];
    C --> D["return null"];
    D --> E["return null"];
    E --> F["return null"];
</pre>
<script src="https://cdn.jsdelivr.net/npm/mermaid@10.9.1/dist/mermaid.min.js"></script>



