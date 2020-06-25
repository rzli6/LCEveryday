# 1333. Filter Restaurants by Vegan-Friendly, Price and Distance

2020/06/22 ZLY

### Problem Description


Given the array `restaurants` where  `restaurants[i] = [idi, ratingi, veganFriendlyi, pricei, distancei]`. You have to filter the restaurants using three filters.

The `veganFriendly` filter will be either *true* (meaning you should only include restaurants with `veganFriendlyi` set to true) or *false* (meaning you can include any restaurant). In addition, you have the filters `maxPrice` and `maxDistance` which are the maximum value for price and distance of restaurants you should consider respectively.

Return the array of restaurant ***IDs*** after filtering, ordered by **rating** from highest to lowest. For restaurants with the same rating, order them by ***id*** from highest to lowest. For simplicity `veganFriendlyi` and `veganFriendly` take value *1* when it is *true*, and *0* when it is *false*.




### Algorithm

We first filter the restaurants with the criterion and sort them respect to the rating.



### Code

```python
def filterRestaurants(self, restaurants: List[List[int]], veganFriendly: int, maxPrice: int, maxDistance: int) -> List[int]:
    if not restaurants:
        return []
    result = []
    for i, rating, vF, price, distance in restaurants:
        if not veganFriendly or (vF and veganFriendly):
            if price <= maxPrice and distance <= maxDistance:
                result.append([i, rating])
    return [i for (i, rating) in sorted(result,key = lambda x:(x[1],x[0]), reverse = True)]
```