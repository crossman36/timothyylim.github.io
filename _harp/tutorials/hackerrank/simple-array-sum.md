### simple array sum

c++

```
int main(){
    int n;
    cin >> n;
    vector<int> arr(n);
    for(int arr_i = 0;arr_i < n;arr_i++){
       cin >> arr[arr_i];
    }
  
    int sum = 0; 
  
    for(int i = 0; i < n; i++){
      sum += arr[i];    
    }  
  
    cout << sum;
  
    return 0;
}
```

php

```
<?php

$handle = fopen ("php://stdin","r");
fscanf($handle,"%d",$n);
$arr_temp = fgets($handle);
$arr = explode(" ",$arr_temp);
array_walk($arr,'intval');

$i = 0;

foreach ($arr as $key => $item) {
    $i += $item;
}

echo $i; 


?>
```
