# Mock 04 | 09/11/2022 | Vincenzo vs ggigazz

## Exercise description

Given the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer.
Return 1 if there is a cycle in the linked list. Otherwise, return 0.

Example1:

    3 -> 2 -> 0 -> -4
        ^          |
        |          |
        ------------

Output: 1

Example2:

    1 -> 2
    ^    |
    ------

Output: 1

Example3

    1

Output: 0

The number of the nodes in the list is in the range [0, 104].
-105 <= Node.val <= 105

### Links & material
- Problem: https://leetcode.com/problems/linked-list-cycle/description/
- Solution: https://leetcode.com/problems/linked-list-cycle/solutions/1829489/c-easy-to-understand-2-pointer-fast-slow/?orderBy=hot
- Follow up: https://leetcode.com/problems/linked-list-cycle-ii/
- Solution: https://leetcode.com/problems/linked-list-cycle-ii/solutions/1701128/c-java-python-slow-and-fast-image-explanation-beginner-friendly/?orderBy=hot


## Interview solution

```c
struct ListNode {
      int val;
      struct ListNode *next;
 };

int checkCycle(struct ListNode *head){
	int flag = 0;
	//outer cycle
    for(struct ListNode *node = head; *node != NULL; node = node->next){
    	struct ListNode *toBeChecked = node;
    	//inner cycle
        for(struct ListNode *innerNode = node; innerNode != NULL; innerNode = innerNode->next){
        	//check the address, if equal break and return 1
            if(toBeChecked == innerNode){
            	//condition of termination
            	flag = 1;
                break;
            }
        }
        if(flag == 1){
			break;
        }
    }

	return flag;
}

```
