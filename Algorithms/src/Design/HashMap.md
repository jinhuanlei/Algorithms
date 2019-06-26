## Design a HashMap

Data structures : Array of buckets
Collision : Separate chaining

code:
```java
class MyHashMap{
	// 因为key的类型是String equals 和 hashCode已经实现好了 所以我们不用去实现
	public class Node{
		final String key;
		Integer value;
		Node next;
		public Node(String key, Integer value){
			this.key = key;
			this.value = value;
		}
	}
	Node[] hashMap;
	int size;
	float loadFactor;
	public static final float DEFAULT_LOAD_FACTOR = 0.75f;
	public static final int DEFAULT_CAPACITY = 10;

	public MyHashMap(){
		this(DEFAULT_LOAD_FACTOR, DEFAULT_CAPACITY);
	}

	public MyHashMap(float loadFactor, int capacity){
		size = 0;
		this.loadFactor = loadFactor;
		this.hashMap = new Node[capacity];
	}
	
	public int size(){
		return size;
	}

	public boolean isEmpty(){
		return size == 0;
	}

	public Integer put(String key, Integer value){
		// will return the old value
		int index = hash(key) % hashMap.length;
		Node head = hashMap[index];
		Node cur = head;
		while(cur != null){
			if(equalsKey(cur.key, key)){
				Integer oldValue = cur.value;
				cur.value = value;
				return oldValue;
			}
			cur = cur.next;
		}
		Node newHead = new Node(key, value);
		newHead.next = head;
		hashMap[index] = newHead;
		size++;
		if(needRehashing()){
			rehashing();
		}
		return null;
	}

	public void rehashing(){
		Node[] newArr = new Node[hashMap.length * 2];
		// for each node in the old array
		// do the put() operation to the new larger array
		// average O(N) worst O(N ^ 2)
	}

	public Integer remove(String key){
		int index = hash(key) % hashMap.length;
		Node head = hashMap[index];
		if(equalsKey(head.key, key)){
			hashMap[index] = head.next;
			size--;
			return head.value;
		}
		Node cur = head;
		Node pre = null;
		while(cur != null){
			if(equalsKey(cur.key, key)){
				pre.next = cur.next;
				size--;
				return cur.value;
			}
			pre = cur;
			cur = cur.next;
		}
		return null;
	}

	public boolean needRehashing(){
		float curLoadFactor = (size + 0.0f) / hashMap.length;
		return curLoadFactor > loadFactor;
	}

	public Integer get(String key){
		int index = hash(key) % hashMap.length;
		Node head = hashMap[index];
		Node cur = head;
		while(cur != null){
			// cur.key is possible null so we can not dereference cur.key
			if(equalsKey(cur.key, key)){
				return cur.value;
			}
			cur = cur.next;
		}
		return null;	
	}

	public boolean equalsKey(String str1, String str2){
		if(str1 == null && str2 == null){
			return true;
		}else if(str1 == null || str2 == null){
			return false;
		}
		return str1.equals(str2);
	}

	public int hash(String str){
		if(str == null){
			return 0;
		}
		return str.hashCode() % 0x7fffffff;
	}

    public static void main(String[] args) {
        MyHashMap hm = new MyHashMap();
        hm.put("a", 1);
        hm.put("b", 2);
        hm.put("c", 3);
        hm.put("d", 4);
        hm.get("A");
        hm.remove("a");
        System.out.println();
    }
}
```