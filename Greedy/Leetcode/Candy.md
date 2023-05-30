### `Problem explain`

There are n children standing in a line. Each child is assigned a rating value given in the integer array ratings.

You are giving candies to these children subjected to the following requirements:

Each child must have at least one candy.

Children with a higher rating get more candies than their neighbors.

Return the minimum number of candies you need to have to distribute the candies to the children.


----

### `Constraints`

n == ratings.length
1 <= n <= 2 * 104
0 <= ratings[i] <= 2 * 104

### `Input/Output Example`

<img width="375" alt="image" src="https://github.com/CodingGuysGroup/Subin/assets/84978165/abacfaa9-fc95-48ee-a72d-67a128733e85">
----


```python
class Solution(object):
    def candy(self, ratings):
        enum_ratings = [1]*len(ratings)
        
        left_candy = 1
        for i in range(1,len(ratings)):
            if ratings[i] > ratings[i-1]:
                left_candy += 1
            else:
                left_candy =1
            enum_ratings[i] = left_candy

        right_candy = 1
        for i in range(len(ratings)-2, -1, -1):
            if ratings[i] > ratings[i+1]:
                right_candy += 1
            else:
                right_candy = 1
            enum_ratings[i] = max(right_candy,enum_ratings[i])
        #print(enum_ratings)
        return sum(enum_ratings)
            

```

<img width="382" alt="image" src="https://github.com/CodingGuysGroup/Subin/assets/84978165/0f13fd59-7379-40ad-b672-56da27c5ebba">



