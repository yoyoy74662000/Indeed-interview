# Indeed-interview
Java, Algorithm

[1 twosum] [Easy]使用 HashMap✅
```java
 public int[] twoSum(int[] nums, int target) {
        if(nums == null || nums.length == 0) return null;
        int[] res = new int[2];
        HashMap<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++){
            if(map.containsKey(target - nums[i])){
                res[0] = map.get(target - nums[i])  ;
                res[1] = i;
            }else{
                map.put(nums[i], i);
            }
        }
        return res;
 }
```
[20 Valid Parentheses] [Easy]使用 Stack✅
```java
public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        for(Character ch : s.toCharArray()){
            if(ch == '('){
                stack.push(')');
            }else if(ch == '['){
                stack.push(']');
            }else if(ch == '{'){
                stack.push('}');
            }else if(stack.isEmpty() || stack.pop() != ch){
                return false;
            }
            
        }
        return stack.isEmpty();
    }
```
