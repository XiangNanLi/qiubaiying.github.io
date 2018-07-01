---
layout:     post
title:      两数之和算法
subtitle:   
date:       2018-07-01
author:     
catalog: true
tags:
	- 算法
    
---


## Problem
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.
Example:

	'''
	Given nums = [2, 7, 11, 15], target = 9,
	Because nums[0] + nums[1] = 2 + 7 = 9,
	return [0, 1].
	'''

## Solution
>C Code:

	'''
	int* twoSum(int* nums, int numsSize, int target) {
	    int *result = malloc(sizeof(int) * 2);
	    for (int i = 0; i < numsSize; i++) {
	        int num_i = nums[i];
	        for (int j = i + 1; j < numsSize; j++) {
	        	int num_j = nums[j];
	        	if (num_i + num_j == target) {
	        		result[0] = i;
	        		result[1] = j;
	        		return result;
	        	}
	        }
	     }
	     return result;
	 }
	'''
This is the slowest solution.
The time complexity:<i>O(n<sup>2</sup>)</i>, because I have two loop to the array. 
The space complexity:<i>O(1)</i>.

###One-pass Hash Table
First loop the array to make a hask table that contais the key(the num) and the value (the index of num). And check out the value of the target minus num if exist in the hash table. If exist ,return the value of the minus result and the value of the num.

>Python Code:

	'''
	class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        dic = {}
        for i in range(len(nums)):
            num_i = nums[i]
            diff = target - num_i
            if dic.__contains__(diff):
                return [dic[diff], i]
            else:
                dic[num_i] = i
        return []
	'''
> C Code(This is from [leetcode.com](https://leetcode.com/)):

	'''
	/**
	 * Note: The returned array must be malloced, assume caller calls free().
	 */
	typedef struct Node{
	    int key;
	    int value;
	    struct Node* next;
	}Node;
	
	typedef struct HashSet{
	    int mapSize;
	    Node** table;
	}HashSet;
	
	void initMap(HashSet* set, int mapSize){
	    set->mapSize=mapSize;
	    set->table = (Node**)malloc(sizeof(Node*) * mapSize);
	    memset(set->table,0,sizeof(Node*) * mapSize);
	}
	
	bool addData(HashSet* set,int key,int value){
	    int hash = key > 0 ? key : -key;
	    hash%=set->mapSize;
	    Node *ptr = set->table[hash];
	
	    while(ptr!=NULL){
	        if(ptr->key==key){
	            return false;
	        }
	        ptr=ptr->next;
	    }
	    ptr=malloc(sizeof(Node));
	    ptr->key=key;
	    ptr->value=value;
	    ptr->next=set->table[hash];
	    set->table[hash]=ptr;
	
	    return true;
	}
	
	bool containsKey(HashSet* set, int key){
	    int hash = key>0 ? key:-key;
	    hash%=set->mapSize;
	    Node* ptr=set->table[hash];
	
	    while(ptr!=NULL){
	        if(ptr->key==key){
	            return true;
	        }
	        ptr=ptr->next;
	    }
	    return false;
	}
	
	int getValue(HashSet* set,int key){
	    int hash = key>0 ? key:-key;
	    hash%=set->mapSize;
	    Node* ptr=set->table[hash];
	
	    while(ptr!=NULL){
	        if(ptr->key==key){
	            return ptr->value;
	        }
	        ptr=ptr->next;
	    }
	
	    return 0;
	
	}
	
	int* twoSum(int* nums, int numsSize, int target) {
	    HashSet map;
	    initMap(&map,numsSize);
	    int* ret = (int*)malloc(sizeof(int)*2);
	    for(int i=0;i<numsSize;i++){
	        if(containsKey(&map,target-nums[i])){
	            ret[0]=getValue(&map,target-nums[i]);
	            ret[1]=i;
	            return ret;
	        }
	        else{
	            addData(&map,nums[i],i);
	        }
	    }
	    return -1;
	}
	'''
	
This is the fastest solution in [leetcode.com](https://leetcode.com/) . This contains make hash and the hash method.

## Review
Last week I test the question use java、 python、swift and c. But if  I use python, the site tells me "Time Limit Exceeded"..., so I make it with the second solution.

Working:1.Creat a ViewController with OC and Swift, but I found the size of the vc's view is confirm in swift code, is 600 * 600 in oc code. Don't know why ?

2.In the C , the length of the struct is the sum of the all element 's size . I copyed the object_class struct and renamed my_object_class, then Convert the address to the struct info. Now I can handle the value by myself , not use the system method.


##Technique
[HashMap](https://zh.wikipedia.org/wiki/%E5%93%88%E5%B8%8C%E8%A1%A8)

Don't know the best way of do it? So just finish it first. Then review it.