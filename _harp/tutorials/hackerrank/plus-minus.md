### plus minus

Given an array of integers, calculate which fraction of the elements are positive, negative, and zeroes, respectively. Print the decimal value of each fraction.

***Input Format***

The first line, NN, is the size of the array. 
The second line contains NN space-separated integers describing the array of numbers.

***Output Format***

Print each value on its own line with the fraction of positive numbers first, negative numbers second, and zeroes third.

Sample Input
```
6
-4 3 -9 0 4 1         
```

Sample Output
```
0.500000
0.333333
0.166667
```

Explanation

There are 3 positive numbers, 2 negative numbers, and 1 zero in the array. 
The fraction of the positive numbers, negative numbers and zeroes are 3/6=0.500000, 2/6=0.33333326=0.333333 and 1/6=0.166667 respectively.

c++
```
int main(){
    int n;
    cin >> n;
    vector<int> arr(n);
    for(int arr_i = 0;arr_i < n;arr_i++){
       cin >> arr[arr_i];
    }
    
    double negatives = 0;
    double zeroes = 0;
    double positives = 0;
    
    for(int i =0; i < n; i++){
        if(arr[i] < 0) negatives++;
        if(arr[i]==0) zeroes++;
        if(arr[i] > 0) positives++;
    }
    
    cout << positives/n << endl;
    cout << negatives/n << endl;
    cout << zeroes/n << endl;
    
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

$negatives = 0;
$zeroes = 0;
$positives = 0;

for ($i=0; $i<$n; $i++){
    if($arr[$i] < 0) $negatives++;
    if($arr[$i] == 0) $zeroes++;
    if($arr[$i] >0 ) $positives++;
}

echo $positives/$n. PHP_EOL . $negatives/$n . PHP_EOL . $zeroes/$n;

?>
```


