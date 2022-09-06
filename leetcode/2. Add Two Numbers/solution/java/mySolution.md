```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
import java.math.*;

class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        String number1 = getNumber(l1);
        String number2 = getNumber(l2);
        BigInteger sumNumber = getSumNumber(number1, number2);
        if (sumNumber.equals(0)) {
            return new ListNode(0);
        }
        return getResult(sumNumber);
    }
    
    private String getNumber(ListNode listNode) {
        StringBuilder sb = new StringBuilder();
        ListNode tempListNode = listNode;
        
        while(true) {
            sb.append(tempListNode.val);
            if (tempListNode.next == null) break;
            tempListNode = tempListNode.next;
        }
        return sb.reverse().toString();
    }
    
    private BigInteger getSumNumber(String n1, String n2) {
        return new BigInteger(n1).add(new BigInteger(n2));
    }
    
    private ListNode getResult(BigInteger sumNumber) {
        char[] digits = String.valueOf(sumNumber).toCharArray();
        ListNode result = null;
        
        for (int i = 0; i < digits.length; i++) {
            if (i == 0) {
                result = new ListNode(Character.getNumericValue(digits[i]));
            } else {
                result = new ListNode(Character.getNumericValue(digits[i]), result);
            }
        }
        return result;
    }
}
```
