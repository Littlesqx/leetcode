## Pascal's Triangle

> Given numRows, generate the first numRows of Pascal's triangle.
> 
>  For example, given numRows = 5,
  Return
  ```Go
  [
         [1],
        [1,1],
       [1,2,1],
      [1,3,3,1],
     [1,4,6,4,1]
  ]
  ```
  **关键**
  
  - 第k层有k个元素
  - 每层第一个以及最后一个元素值为1
  - 对于第k（k > 2）层第n（n > 1 && n < k）个元素A[k][n]，A[k][n] = A[k-1][n-1] + A[k-1][n]
  
  **解法**
  
  ```Go
  func generate(numRows int) [][]int {
      triangle := make([][]int, numRows)
      for i := 0; i < numRows; i++ {
      	triangle[i] = make([]int, i+1)
      	triangle[i][0] = 1
      	triangle[i][i] = 1
      	for j := 1; j < i; j++ {
      		triangle[i][j] = triangle[i-1][j-1] + triangle[i-1][j]
      	}
      }
      return triangle
  }
  ```