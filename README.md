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
[21 Merge Two Sorted Lists] [Easy]使用 dummy✅
```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        dummy.next = merge(l1,l2);
        return dummy.next;
    }
    
    public ListNode merge(ListNode p, ListNode q){
        ListNode dummy = new ListNode(0);
        ListNode cur = dummy;
        while(p != null && q != null){
            if(p.val <= q.val){
                cur.next = new ListNode(p.val);
                p = p.next;
                cur = cur.next;
            }else{
                cur.next = new ListNode(q.val);
                q = q.next;
                cur = cur.next;
            }
        }
        if(p == null){
            cur.next = q;
        }else{
            cur.next = p;
        }
        return dummy.next;
    }
```
[23 Merge k Sorted Lists] [Hard]使用 dummy✅
```java
public ListNode mergeKLists(ListNode[] lists) {
        if(lists == null) return null;
        int len = lists.length;
        if(len == 0) return null;
        ListNode dummy = new ListNode(0);
        ListNode cur = dummy;
        dummy.next = lists[0];
        for(int i = 1; i < len; i++){
            cur.next = merge(dummy.next, lists[i]);
        }
        return dummy.next;
    }
    
    public ListNode merge(ListNode p, ListNode q){
        ListNode dummy = new ListNode(0);
        ListNode cur = dummy;
        while(p != null && q != null){
            if(p.val <= q.val){
                cur.next = new ListNode(p.val);
                p = p.next;
                cur = cur.next;
            }else{
                cur.next = new ListNode(q.val);
                q = q.next;
                cur = cur.next;
            }
        }
        if(p == null){
            cur.next = q;
        }else{
            cur.next = p;
        }
        return dummy.next;
    }
```
[56 Merge Intervals] [Medium] 轉換成 Array✅
```java
public List<Interval> merge(List<Interval> intervals) {
        // sort start&end
        int n = intervals.size();
        int[] starts = new int[n];
        int[] ends = new int[n];
        for (int i = 0; i < n; i++) {
            starts[i] = intervals.get(i).start;
            ends[i] = intervals.get(i).end;
        }
        Arrays.sort(starts);
        Arrays.sort(ends);
        // loop through
        List<Interval> res = new ArrayList<Interval>();
        for (int i = 0, j = 0; i < n; i++) { // j is start of interval.
            if (i == n - 1 || starts[i + 1] > ends[i]) {
                res.add(new Interval(starts[j], ends[i]));
                j = i + 1;
            }
        }
        return res;
    }
```

[88 Merge Sorted Array] [Easy] Array✅
```java
public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m -1;
        int j = n -1;
        int k = m + n -1;
        while(i >=0 && j >= 0){
            nums1[k] = nums1[i] >= nums2[j] ? nums1[i--] : nums2[j--];
            k--;
        }
        //這個是當num1 > num2
        //num1 [4,5,6]
        //num2 [1,2,3]
        while(j >= 0){
            nums1[k] = nums2[j--];
            k--;
        }
    }
```
[139 Word Break] [Medium] DP 類似雙指針✅
```java
public boolean wordBreak(String s, List<String> wordDict) {
        boolean[] f = new boolean[s.length() + 1];
        
        f[0] = true;
        for(int i=1; i <= s.length(); i++){
            for(int j=0; j < i; j++){
                if(f[j] && wordDict.contains(s.substring(j, i))){
                    f[i] = true;
                    break;
                }
            }
        }
        
        return f[s.length()];
    }
