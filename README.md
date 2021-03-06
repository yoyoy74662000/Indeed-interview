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
```
[224 Basic Calculators] [Hard] stack ✅
```java
public int calculate(String s) {
        Stack<Integer> stack = new Stack<>();
        int sign = 1;
        int res = 0;
        for (int i = 0; i < s.length(); i++) {
            if (Character.isDigit(s.charAt(i))) {
                int num = s.charAt(i) - '0';
                while (i + 1 < s.length() && Character.isDigit(s.charAt(i + 1))) {
                    num = num * 10 + s.charAt(i + 1) - '0';
                    i++;
                }
                res += num * sign;
            } else if (s.charAt(i) == '+') {
                sign = 1;
            } else if (s.charAt(i) == '-') {
                sign = -1;
            } else if (s.charAt(i) == '(') {
                stack.push(res);
                stack.push(sign);
                res = 0;
                sign = 1;
            } else if (s.charAt(i) == ')') {
                res = res * stack.pop() + stack.pop();
            }
        }
        return res;

    }
```

[228 Summary Ranges] [Medium] 前後 array ✅
```java
public List<String> summaryRanges(int[] nums) {
        List<String> list=new ArrayList();
        if(nums.length==1){
            list.add(nums[0]+"");
            return list;
        }
        for(int i=0;i<nums.length;i++){
            int a=nums[i];
            while(i+1<nums.length&&(nums[i+1]-nums[i])==1){
                i++;
            }
            if(a!=nums[i]){
                list.add(a+"->"+nums[i]);
            }else{
                list.add(a+"");
            }
        }
        return list;
    }
```
[243 Shortest Word Distance] [Easy] two for loop 類似指針 ✅
```java
public int shortestDistance(String[] words, String word1, String word2) {
        int res = words.length;
        for(int i = 0; i < words.length; i++){
            if(words[i].equals(word1)){
                for(int j = 0; j < words.length; j++){
                    if(words[j].equals(word2)){
                        res = Math.min(res, Math.abs(i-j));
                    }
                }
            }
        }
        return res;
    }
```
[244	Shortest Word Distance II] [Medium] HashMap to record 位置 ✅
```java
private Map<String, List<Integer>> map;

    public WordDistance(String[] words) {
        map = new HashMap<String, List<Integer>>();
        for(int i = 0; i < words.length; i++) {
            String w = words[i];
            if(map.containsKey(w)) {
                map.get(w).add(i);
            } else {
                List<Integer> list = new ArrayList<Integer>();
                list.add(i);
                map.put(w, list);
            }
        }
    }

    public int shortest(String word1, String word2) {
        List<Integer> list1 = map.get(word1);
        List<Integer> list2 = map.get(word2);
        int ret = Integer.MAX_VALUE;
        for(int i = 0, j = 0; i < list1.size() && j < list2.size(); ) {
            int index1 = list1.get(i), index2 = list2.get(j);
            if(index1 < index2) {
                ret = Math.min(ret, index2 - index1);
                i++;
            } else {
                ret = Math.min(ret, index1 - index2);
                j++;
            }
        }
        return ret;
    }
```
[245	Shortest Word Distance III] [Medium] for loop 裡面用 if if if 類似 指針 ✅
```java
public int shortestWordDistance(String[] words, String word1, String word2) {
        int a = -1, b = -1;
        int res = words.length;
        for(int i = 0; i < words.length; i++){
            if(words[i].equals(word1)){
                a = i;
            }
            if(words[i].equals(word2)){
                if(word1.equals(word2)){
                    a = b;
                }
                b = i;
            }
            if(a != -1 && b != -1){
                res = Math.min(res, Math.abs(a-b));
            }
        }
        return res;
    }
```
[346 Moving Average from Data Stream] [Easy] Queue ✅
```java
private double previousSum = 0.0;
    private int maxSize;
    private Queue<Integer> currentWindow;
    /** Initialize your data structure here. */
    public MovingAverage(int size) {
        currentWindow = new LinkedList<Integer>();
        maxSize = size;
    }
    
    public double next(int val) {
        if(currentWindow.size() == maxSize){
            previousSum -= currentWindow.remove();
            previousSum += val;
            currentWindow.add(val);
        } else{
            previousSum += val;
            currentWindow.add(val);
        }
        return previousSum / currentWindow.size();
    }
```
[453 Minimum Moves to Equal Array Elements] [Easy] Math problem ✅
```java
public int minMoves(int[] nums) {
        if (nums.length == 0) return 0;
        int min = nums[0];
        for (int n : nums) min = Math.min(min, n);
        int res = 0;
        for (int n : nums) res += n - min;
        return res;
    }
```
[563 Binary Tree Tilt] [Easy] tree post order ✅
```java
int result = 0;

    public int findTilt(TreeNode root) {
        postOrder(root);
        return result;
    }

    private int postOrder(TreeNode root) {
        if (root == null) return 0;

        int left = postOrder(root.left);
        int right = postOrder(root.right);

        result += Math.abs(left - right);

        return left + right + root.val;
    }
```
[657 Robot Return to Origin] [Easy] if else ✅
```java
public boolean judgeCircle(String moves) {
        int x = 0;
        int y = 0;
        for (char ch : moves.toCharArray()) {
            if (ch == 'U') y++;
            else if (ch == 'D') y--;
            else if (ch == 'R') x++;
            else if (ch == 'L') x--;
        }
        return x == 0 && y == 0;
    }

```
[811	Subdomain Visit Count] [Easy] HashMap ✅
```java
public List<String> subdomainVisits(String[] cpdomains) {
        List<String> res = new ArrayList();
        Map<String, Integer> counts = new HashMap();
        
        for (String cpdomain : cpdomains) {
            String[] countDomain = cpdomain.split(" ");
            int count = Integer.parseInt(countDomain[0]);
            String domain = countDomain[1];
            
            counts.put(domain, counts.getOrDefault(domain, 0) + count);
            for (int i = 0; i < domain.length(); i++) {
                if (domain.charAt(i) == '.') {
                    String subdomain = domain.substring(i + 1);
                    counts.put(subdomain, counts.getOrDefault(subdomain, 0) + count);
                }
            }
        }
        
        for (Map.Entry<String, Integer> entry : counts.entrySet()) {
            res.add(entry.getValue() + " " + entry.getKey());
        }
        return res;        
    }

```
[ReverseStringButHtml] [medium]使用 Swap✅
```java
public static void main(String[] args) {
	ReverseStringButHtml sol = new ReverseStringButHtml();
	String s = "3&TWD;2&J";
	System.out.println(sol.reverseHtml(s));
}
 public String reverseHtml(String html) {
	if (html == null || html.length() == 0) {
		return null;
	}
	int len = html.length();
	char[] chArr = html.toCharArray();
	swap(chArr, 0, len - 1);
	int start = 0;
	int end = 0;
	while (end < len) {
		if (chArr[end] == ';') {
		start = end;
		} else if (chArr[end] == '&') {
			if (chArr[start] == ';'){
				swap(chArr, start, end);
			}
		start = end + 1;
		}
		end++;
	}
	return new String(chArr);
}
 private void swap(char[] chars, int start, int end) {
	while (start < end) {
		char temp = chars[start];
		chars[start++] = chars[end];
		chars[end--] = temp;
	}
}
```
