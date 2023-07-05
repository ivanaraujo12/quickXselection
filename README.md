# quickXselection

import random
import time

def generate_data(size, sorted=False, partially_sorted=False):
    data = list(range(1, size + 1))
    
    if not sorted:
        random.shuffle(data)
    
    if partially_sorted:
        
        for _ in range(size // 10):
            i, j = random.randint(0, size - 1), random.randint(0, size - 1)
            data[i], data[j] = data[j], data[i]
    
    return data

def quicksort(data):
    if len(data) <= 1:
        return data

    pivot = data[random.randint(0, len(data)-1)]
    less = []
    equal = []
    greater = []

    for element in data:
        if element < pivot:
            less.append(element)
        elif element == pivot:
            equal.append(element)
        else:
            greater.append(element)

    return quicksort(less) + equal + quicksort(greater)

def selectionsort(data):
    for i in range(len(data)):
        min_index = i

        for j in range(i+1, len(data)):
            if data[j] < data[min_index]:
                min_index = j

        data[i], data[min_index] = data[min_index], data[i]

    return data


data_size = 50000
data_sorted = generate_data(data_size, sorted=True)
data_partially_sorted = generate_data(data_size, partially_sorted=True)
data_random = generate_data(data_size)


start_time = time.time()
quicksort(data_sorted.copy())
quicksort_sorted_time = time.time() - start_time

start_time = time.time()
quicksort(data_partially_sorted.copy())
quicksort_partially_sorted_time = time.time() - start_time

start_time = time.time()
quicksort(data_random.copy())
quicksort_random_time = time.time() - start_time


start_time = time.time()
selectionsort(data_sorted.copy())
selectionsort_sorted_time = time.time() - start_time

start_time = time.time()
selectionsort(data_partially_sorted.copy())
selectionsort_partially_sorted_time = time.time() - start_time

start_time = time.time()
selectionsort(data_random.copy())
selectionsort_random_time = time.time() - start_time


print(f"Quicksort - Sorted data: {quicksort_sorted_time} seconds")
print(f"Quicksort - Partially sorted data: {quicksort_partially_sorted_time} seconds")
print(f"Quicksort - Random data: {quicksort_random_time} seconds")
print()
print(f"Selectionsort - Sorted data: {selectionsort_sorted_time} seconds")
print(f"Selectionsort - Partially sorted data: {selectionsort_partially_sorted_time} seconds")
print(f"Selectionsort - Random data: {selectionsort_random_time} seconds")
