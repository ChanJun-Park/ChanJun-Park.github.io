---
title: "[LeetCode] Trapping Rain Water"
date: 2020-09-25T15:34:30-04:00
classes: wide
categories:
  - Algorithm Problem Solving
tags:
  - Two Pointer
---

[문제링크](https://leetcode.com/problems/trapping-rain-water/)

i번째 인덱스 지점에 고여있는 물은 `min(왼쪽에 있는 기둥의 최대값, 오론쪽에 있는 기둥의 최대값) - i번째 기둥의 높이` 로 구할 수 있다. 미리 i번째 지점에서 왼쪽 오른쪽 기둥의 최대값을 구해놓고 배열을 순회하여 문제를 풀 수 있다. 그런데 어느 한 지점에 대해서 왼쪽 오른쪽 기둥 중 높이가 더 작은 기둥을 기준으로 물이 고여있게 된다는 점을 이용하면 미리 왼쪽 오른쪽 최대값을 구하지 않고 문제를 풀 수 있다. `left`, `right` 라는 두 개의 포인터를 이용해서, `height[left] < height[right]` 일 때는 `left` 지점에서 오른쪽에 `height[right]` 크기의 기둥이 물을 고여있게 할 수 있다. 따라서 `left` 왼쪽 지점에 있는 기둥의 최대값만 구해서 `leftMax - i번째 기둥의 높이`를 답에 누적하는 식으로 문제를 해결할 수 있다.

투 포인터 알고리즘을 이용한 풀이

풀이

```java
class Solution {
    public int trap(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int leftMax = 0;
        int rightMax = 0;
        int ans = 0;
        
        while(left < right) {
            if (height[left] < height[right]) {
                if (height[left] >= leftMax) {
                    leftMax = height[left];
                } else {
                    ans += (leftMax - height[left]);
                }
                left++;
            } else {
                if (height[right] >= rightMax) {
                    rightMax = height[right];
                } else {
                    ans += (rightMax - height[right]);
                }
                right--;
            }
        }
        
        return ans;
    }
}
```
