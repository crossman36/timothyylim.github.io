### diagnonal difference

Given a square matrix of size N×N , calculate the absolute difference between the sums of its diagonals.

**Input Format**

The first line contains a single integer, N . The next N lines denote the matrix's rows, with each line containing N space-separated integers describing the columns.

**Output Format**

Print the absolute difference between the two sums of the matrix's diagonals as a single integer.

Sample Input
```
3
11 2 4
4 5 6
10 8 -12
```
Sample Output
```
15
```

**Explanation**

The primary diagonal is: 
```
11
      5
            -12
```
Sum across the primary diagonal: 11 + 5 - 12 = 4

The secondary diagonal is:
```
            4
      5
10
```
Sum across the secondary diagonal: 4 + 5 + 10 = 19 
Difference: |4 - 19| = 15

c++

```
int main(){
    int n;
    cin >> n;
    vector< vector<int> > a(n,vector<int>(n));
    for(int a_i = 0;a_i < n;a_i++){
       for(int a_j = 0;a_j < n;a_j++){
          cin >> a[a_i][a_j];
       }
    }
  
    int sum_a=0;
    int sum_b=0;
  
    for(int i=0; i<n; i++)
      sum_a += a[i][i];
  
    for(int i=0; i<n; i++)
      sum_b += a[n-i-1][i];

    cout << abs(sum_a-sum_b);
    
    return 0;
}

```

php

```
<?php

$handle = fopen ("php://stdin","r");
fscanf($handle,"%d",$n);
$a = array();
for($a_i = 0; $a_i < $n; $a_i++) {
   $a_temp = fgets($handle);
   $a[] = explode(" ",$a_temp);
  array_walk($a[$a_i],'intval');
}


$sum_a = 0;
$sum_b = 0;

for($i=0;$i<$n;$i++){
    $sum_a += $a[$i][$i];
}


for($i=0;$i<$n;$i++){
    $sum_b += $a[$n-$i-1][$i];
}

echo abs($sum_a-$sum_b);
?>
```


