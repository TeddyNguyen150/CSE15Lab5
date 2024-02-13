```
import org.junit.*;
import static org.junit.Assert.*;

public class LinkedListMyTests {
    LinkedList oneElementList;
    LinkedList twoElementList;

    @Before
    public void setUp(){
        oneElementList = new LinkedList();
        oneElementList.root = new Node(1, null);

        twoElementList = new LinkedList();
        twoElementList.root = new Node(10, null);
        twoElementList.root.next = new Node(20, null);
    }


	@Test 
	public void testAppendOneElement() {
    oneElementList.append(2);
    assertEquals(2, oneElementList.root.next.value);
	}

	@Test 
	public void testAppendTwoElement() {
    twoElementList.append(30);
    assertEquals(20, twoElementList.root.next.value);
    assertEquals(30, twoElementList.root.next.next.value);
	}
}
```

![image](https://github.com/TeddyNguyen150/CSE15Lab5/assets/156158048/7f78b57e-8c06-4a02-bc7e-e62134e22f51)

```//before
    public void append(int value) {
        if(this.root == null) {
            this.root = new Node(value, null);
            return;
        }
        // If it's just one element, add if after that one
        Node n = this.root;
        if(n.next == null) {
            n.next = new Node(value, null);
            return;
        }
        // Otherwise, loop until the end and add at the end with a null
        while(n.next != null) {
            n = n.next;
            n.next = new Node(value, null);
        }
    }
```

```//after
    public void append(int value) {
        if(this.root == null) {
            this.root = new Node(value, null);
            return;
        }
        // If it's just one element, add if after that one
        Node n = this.root;
        if(n.next == null) {
            n.next = new Node(value, null);
            return;
        }
        // Otherwise, loop until the end and add at the end with a null
        while(n.next != null) {
            n = n.next;
        }
        n.next = new Node(value, null);
    }
```

The reason why the fix works is because previously, it kept on instantiating a new n.next so that the while loop sees that n.next is never null,
but with the fix it properly sets n.next when it reaches the end.

--Part 2--

1. grep -n (lines where a pattern is)
```
$ grep -n "rr" find-results.txt
830:technical/biomed/rr166.txt
831:technical/biomed/rr167.txt
832:technical/biomed/rr171.txt
833:technical/biomed/rr172.txt
834:technical/biomed/rr191.txt
835:technical/biomed/rr196.txt
836:technical/biomed/rr37.txt
837:technical/biomed/rr73.txt
838:technical/biomed/rr74.txt

$grep -n "glutamate" ./technical/biomed/*.txt
"A lot"
```
This is useful if you want to read a specific portion of a txt file with the word in it without using ctrl + f

2. grep -L (files without the following string)

```
$ grep -L "glutamate" ./technical/biomed/*.txt
"A lot"

$ grep -L "rr" ./technical/biomed/*.txt
./technical/biomed/1471-2105-3-24.txt
./technical/biomed/1471-2156-2-3.txt
./technical/biomed/1471-2490-3-2.txt
./technical/biomed/1472-6947-1-5.txt
./technical/biomed/1472-6963-3-11.txt
```
This is useful to know if there are files without a specific word or pattern, like how there are 5 files in biomed without "rr" anywhere in them.

3. grep -i (ignore case)
```
$ grep -i "i" ./technical/biomed/*.txt | wc
 412863 3669918 40395656

$ grep -i "cook" ./technical/biomed/*.txt | wc
     19     194    1909
```
Useful to know the exact character amount, because sometimes sentences start with I.

4. grep -l (files with match)
```
$ grep -l "I " ./technical/biomed/*.txt | wc
    579     579   21883

$ grep -l "I" ./technical/biomed/*.txt | wc
    837     837   31490
```

Useful to know which files have the exact sequence of a string
