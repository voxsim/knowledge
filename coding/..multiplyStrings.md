// Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2.

// Note:
// The length of both num1 and num2 is < 110.
// Both num1 and num2 contains only digits 0-9.
// Both num1 and num2 does not contain any leading zero.
// You must not use any built-in BigInteger library or convert the inputs to integer directly.


'''
function multiplyStrings(num1, num2) {
  let carry = 0;
  let result = '';
  for(let i=num2.length-1; i > -1; i--) {
    for(let j=num1.length-1; j > -1; j--) {
       console.log(carry, num2[i],  num1[j], Math.pow(10, num1.length - j -1));
       carry = carry + +(num2[i]) * +(num1[j]) * Math.pow(10, num1.length - j -1);       
    }
    result = (carry % 10) + result;
    carry = Math.floor(carry/10);
  }
  if(carry > 0) {
    result = (carry % 10) + result;
  }
  return result;
}
'''

EXAMPLES:
- multiplyStrings('2', '3') = '6'
- multiplyStrings('2', '5') = '10'
- multiplyStrings('12', '3') = '36'
- multiplyStrings('12', '5') = '60'
- multiplyStrings('12', '11') = '132'
- multiplyStrings('12', '22') = '264'
