---
layout: post
title:  295. Find Median from Data Stream
categories: [Sorting, PriorityQueue]
---

## [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)

The median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value and the median is the mean of the two middle values.

>    For example, for arr = [2,3,4], the median is 3.
>    For example, for arr = [2,3], the median is (2 + 3) / 2 = 2.5.

Implement the MedianFinder class:

    MedianFinder() initializes the MedianFinder object.
    void addNum(int num) adds the integer num from the data stream to the data structure.
    double findMedian() returns the median of all elements so far. Answers within 10-5 of the actual answer will be accepted.



***Example 1:***

>Input
>["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
>[[], [1], [2], [], [3], []]
>Output
>[null, null, null, 1.5, null, 2.0]

>Explanation
>MedianFinder medianFinder = new MedianFinder();
>medianFinder.addNum(1);    // arr = [1]
>medianFinder.addNum(2);    // arr = [1, 2]
>medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)
>medianFinder.addNum(3);    // arr[1, 2, 3]
>medianFinder.findMedian(); // return 2.0


## Solution using PriorityQueues

```c++
class MedianFinder {
    priority_queue<int> max_pq;
    priority_queue<int, vector<int>, greater<int>> min_pq;
public:
    MedianFinder() {

    }

    void addNum(int num) {
        if ((max_pq.size() == 0) || (num < max_pq.top())) {
            max_pq.push(num);
        } else {
            min_pq.push(num);
        }

        if(min_pq.size() > max_pq.size() + 1) {
            max_pq.push(min_pq.top());
            min_pq.pop();
        }
        if(min_pq.size() + 1 < max_pq.size()) {
            min_pq.push(max_pq.top());
            max_pq.pop();
        }
    }

    double findMedian() {   
        if (min_pq.size() == max_pq.size()) {
            return (min_pq.top() + max_pq.top())/2.0;
        } else {
            return (max_pq.size() > min_pq.size())?max_pq.top():min_pq.top();
        }
    }
};
```
