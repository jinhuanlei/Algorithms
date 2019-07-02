## String Shuffling

Utilize the Merge Sort with customize comparison
```java
class Solution{
    public String stringShuffling(String str){
    	// A1B2C3D4 => ABCD1234
    	// MergeSort with customized Comparator
    	// assume size is even number
    	if(str == null || str.length() == 0){
    		return str;
    	}
    	char[] arr = str.toCharArray();
    	char[] helper = new char[arr.length];
    	stringShufflingHelper(arr, helper, 0, arr.length - 1);
        return new String(arr);
    }

    public void stringShufflingHelper(char[] arr, char[] helper, int left, int right){
    	if(left >= right){
    		return;
    	}
    	int mid = left + (right - left) / 2;
    	stringShufflingHelper(arr, helper, left, mid);
    	stringShufflingHelper(arr, helper, mid + 1, right);
    	merge(arr, helper, left, mid, right);
    }

    public void merge(char[] arr, char[] helper, int left, int mid, int right){
    	int index1 = left;
    	int index2 = mid + 1;
    	int cur = left;
    	while(index1 <= mid && index2 <= right){
    		char c1 = arr[index1];
    		char c2 = arr[index2];
    		if(compare(c1, c2) < 0){
                helper[cur++] = c1;
                index1++;
    		}else{
                helper[cur++] = c2;
                index2++;
    		}
    	}
    	while(index1 <= mid){
    		helper[cur++] = arr[index1++];
    	}
    	while(index2 <= right){
    		helper[cur++] = arr[index2++];
    	}
    	for(int x = left; x <= right; x++){
    		arr[x] = helper[x];
    	}
    }

    public int compare(Character c1, Character c2){
    	if(Character.isLetter(c1) && Character.isLetter(c2)){
    		return Integer.valueOf(c1 - c2);
    	}else if(Character.isLetter(c1)){
    		return -1;
    	}else if(Character.isLetter(c2)){
            return 1;
        }
    	return Integer.valueOf(c1 - c2);
    }

    public static void main(String args[]){
        Solution s = new Solution();
        System.out.println(s.stringShuffling("A1B23"));
    }
}
```