## Plus One

> Given a non-negative integer represented as a non-empty array of digits, plus one to the integer.
>
> You may assume the integer do not contain any leading zero, except the number 0 itself.
>  
> The digits are stored such that the most significant digit is at the head of the list.

**解法：**
```Go
func plusOne(digits []int) []int {
    carry, sum, n := 1, 0, len(digits)
    for i := n-1; i >= 0; i-- {
    	if digits[i] < 9 {
    		digits[i] = (digits[i] + carry)
    		return digits
    	} else {
    		sum = digits[i] + carry
    		carry = sum / 10
    		digits[i] = sum % 10
    	}
    }
    if carry == 1 {
    	digits = append([]int{1}, digits...)
    }
    return digits
}
```