# LeetcodeAddtwonumbersLinkedlist
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
	ListNode *addTwoNumbers(
		ListNode *l1,
		ListNode *l2,
		ListNode *head = nullptr,
		int carry = 0,
		ListNode *tmp = nullptr) {
		int csum;
		if (l1 == nullptr && l2 == nullptr) {
            if(carry==1)
                tmp->next = new ListNode(carry);
			return head;
		} else if (l1 == nullptr) {
			csum = (l2->val + carry) % 10;
			carry = (l2->val + carry) / 10;
			l2 = l2->next;
		} else if (l2 == nullptr) {
			csum = (l1->val + carry) % 10;
			carry = (l1->val + carry) / 10;
			l1 = l1->next;
		} else {
			csum = (l1->val + l2->val + carry) % 10;
			carry = (l1->val + l2->val + carry) / 10;
			l1 = l1->next;
			l2 = l2->next;
		}
		if (head == nullptr) {
			head = new ListNode(csum);
			tmp = head;
			return addTwoNumbers(l1, l2, head, carry, tmp);
		} else {
			tmp->next = new ListNode(csum);
            tmp = tmp->next;
			return addTwoNumbers(l1, l2, head, carry, tmp);
		}
	}
};
