---
title: "[LeetCode] Container With Most Water"
date: 2020-09-25T15:34:30-04:00
classes: wide
categories:
  - Algorithm Problem Solving
tags:
  - Two Pointer
---

[문제링크](https://leetcode.com/problems/container-with-most-water/)

두 개의 기둥을 선택했을때 항상 길이가 짧은 쪽을 높이로 해서 컨테이너의 넓이가 정해진다는 사실을 이용한다. 가장 바깥쪽을 나타내는 두 개의 포인터를 이용해서 넓이를 구한 다음, 짧은 기둥을 가리키는 포인터를 안쪽으로 이동시킨다. 이때 긴 기둥을 가리키는 포인터를 안쪽으로 이동시키지 않는 이유는, 그렇게 하면 방금전 계산했던 넓이보다 항상 작은 넓이만이 구해지기 때문이다.((1)더 큰 높이를 갖는 기둥이 나타나는 경우 방금전 짧은 길이의 기둥으로 높이를 삼고, 더 짧아진 거리로 가로를 삼아 넓이가 더 작아짐, (2)더 짧은 길이의 기둥이 나타나는 경우 높이도 짧아지고 거리도 짧아져서 넓이가 더 작아짐). 두 포인터가 교차하기 전까지 반복해서 계산하면 모든 경우를 확인할 수 있다.

투 포인터 알고리즘을 이용한 풀이

풀이

```java
class Solution {
    public int maxArea(int[] height) {
        int ans = 0;
        
        int left = 0;
        int right = height.length - 1;
        int temp = 0;
        while(left < right) {
        	
        	if (height[left] > height[right]) {
        		temp = height[right] * (right - left);
        		right--;
        	} else if (height[left] < height[right]) {
        		temp = height[left] * (right - left);
        		left++;
        	} else {        	
        		temp = height[left] * (right - left);
        		right--;
        		left++;
        	}
        	
        	if (ans < temp) ans = temp;
        }
        
    	return ans;
    }
}
```

[증명 관련 링크](https://leetcode.com/problems/container-with-most-water/discuss/6099/yet-another-way-to-see-what-happens-in-the-on-algorithm)
