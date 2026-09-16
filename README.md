# Prosoft_tasks

## Задача 1. Add Two Numbers
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.
You may assume the two numbers do not contain any leading zero, except the number 0 itself.
<img width="500" height="383" alt="image" src="https://github.com/user-attachments/assets/838340b8-ab5d-455e-8806-ea2f8a40923a" />


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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* res = new ListNode(0);
        ListNode* step = res;
        int carry = 0;
        while (l1 != nullptr || l2 != nullptr || carry != 0) {
            int l1Cur = (l1 != nullptr) ? l1->val : 0;
            int l2Cur = (l2 != nullptr) ? l2->val : 0;
            int sum = l1Cur + l2Cur + carry;
            int digit = sum % 10;
            carry = sum / 10;
            step->next = new ListNode(digit);
            step = step->next;
            if (l1 != nullptr)
                l1 = l1->next;
            if (l2 != nullptr)
                l2 = l2->next;
        }
        return res->next;
    }
};


# Решение:
Если приглядеться к картинке в примере к задаче, можно заметить, что цифры в итоговом числе равны сумме цифр на соответствующих разрядах первых двух чисел.
Это значит, что мы можем проходиться по двум имеющимся односвязным спискам, на ходу складывая цифры и записывая их на соответствующие места в результирующем списке
(не забывая про "перенос" - если сумма в моменте окажется больше 9, то в следующий разряд отправится излишек).
Таким образом образуется цикл, работающий до тех пор, пока у нас есть цифры хотя бы в одном списке или недобавленный перенос. Проверками мы обрабатываем случаи,
когда указатель выходит за значащие элементы списка (в nullptr), заменяя такие значения нулем. Digit - цифра, попадающая в текущий разряд, отделяется от всей текущей суммы,
по классике, остатком от деления на 10, а перенос - делением на 10 (чтобы получить первую и "остальные" цифры соответственно (мы уверенны, что сумма не более, чем двузнаковая, так что /10 дает вторую цифру для переноса)).
Если указатель не nullptr, продолжаем его двигать дальше. Если один из списков кончится, все легко - дальше будут просто "переписываться" цифры из оставшегося, пока не кончатся оба.
