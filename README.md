# merge sort demo

## 將 Ordered List L1 , Ordered List L2 merge OrderedList L3

## 想法 首先把 List 變成Array sort之後在逐一 add to List

```javascript===
function ListNode (val, next) {
    this.val = (val === undefined) ? 0: val;
    this.next = (next === undefined) ? null: next;
}
/**
 * mergeSort
 * 
 * @param {ListNode} L1 
 * @param {ListNode} L2 
 * 
 * @return {ListNode}
 */
const mergeSort = (L1, L2) => {
    let ptr1 = L1;
    let ptr2 = L2;
    let target = null;
    let result =[]
    while(ptr1 !== null || ptr2 !== null) {
        const condition = judgeCase(ptr1, ptr2);
        switch (condition) {
            case 0:
                const isL1Small = ptr1.val < ptr2.val;
                if (isL1Small) {
                    result.push(ptr1.val);
                    ptr1 = ptr1.next;
                } else {
                    result.push(ptr2.val);
                    ptr2 = ptr2.next;
                }
                break;       
            case 1: // both null
                return result;
            case 2:  // L1  null
                result.push(ptr2.val);
                ptr2 = ptr2.next;
                break;
            default: // L2 null
                result.push(ptr1.val);
                ptr1 = ptr1.next;
                break;
        }
    }
    if (result.length > 0) {
        target = doPush(result);
    }
    return target;
}
/**
 * judgeCase
 * 
 * @param {ListNode} L1 
 * @param {ListNode} L2
 * 
 * @return {number}
 */
const judgeCase = (L1, L2) => {
    if (L1 !== null && L2 !== null) {
        return 0;
    } else if (L1 === null && L2 === null) {
        return 1;
    } else if (L1 === null) {
        return 2;
    } else {
        return 3;
    }
}

/**
 * transversal
 * @param {ListNode} L 
 */
const transversal =  (L) => {
    while(L !== null) {
        console.log(`${L.val}`)
        L = L.next;
    }
} 
/**
 * doPush
 * 
 * @param {number[]} arr
 * 
 * @return {ListNode} 
 */
const doPush = (arr) => {
    let head = null;
    let target = null;
    arr.forEach( (item)=> {
        if (target == null) {
            target = new ListNode(item, null);
            head = target;
        } else {
            const currentNode = new ListNode(item, null);
            target.next = currentNode;
            target = target.next;
        }
    });
    return head;
};

const L1 = doPush([1, 1]);
const L2 = doPush([1,2,4]);
console.log("===========================================")
const result = mergeSort(L1, L2);
transversal(result);
```