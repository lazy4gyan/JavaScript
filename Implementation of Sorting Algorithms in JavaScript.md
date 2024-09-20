# Implementation of Sorting Algorithms in JavaScript

###### 1. Bubble Sort

Description: Bubble Sort repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The process repeats until the list is sorted.

##### Time Complexity
- Best Case: O(n) (when the array is already sorted)
- Average and Worst Case: O(n<sup>2</sup>)

<details><summary><b>Implementation</b></summary>
<p>

#### Code: 

```javascript
function bubbleSort(arr) {
  let n = arr.length;
  for (let i = 0; i < n - 1; i++) {
    for (let j = 0; j < n - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        // Swap
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
      }
    }
  }
  return arr;
}

const bubbleSortedArray = bubbleSort([2, 2, 2, 0, 0, 0, 1, 1]);
console.log(bubbleSortedArray); // Output: [0, 0, 0, 1, 1, 2, 2, 2]

```

</p>
</details>

---


###### 2. Selection Sort

Description: Selection Sort divides the input list into two parts: a sorted part and an unsorted part. It repeatedly selects the smallest (or largest) element from the unsorted part and moves it to the sorted part.

##### Time Complexity
- Best, Average, and Worst Case: O(n<sup>2</sup>)

<details><summary><b>Implementation</b></summary>
<p>

#### Code: 

```javascript
function selectionSort(arr) {
  let n = arr.length;
  for (let i = 0; i < n - 1; i++) {
    let minIndex = i;
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }
    // Swap the found minimum element with the first element
    [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
  }
  return arr;
}

const selectionSortedArray = selectionSort([2, 2, 2, 0, 0, 0, 1, 1]);
console.log(selectionSortedArray); // Output: [0, 0, 0, 1, 1, 2, 2, 2]

```

</p>
</details>

---

###### 3. Insertion Sort

Description: Insertion Sort builds a sorted array one element at a time by repeatedly taking the next unsorted element and inserting it into the correct position in the sorted part.

##### Time Complexity
- Best Case: 𝑂(𝑛) (when the array is already sorted)
- Average and Worst Case: O(n<sup>2</sup>)

<details>
<summary><b>Implementation</b></summary>
<p>

#### Code: 

```javascript
function insertionSort(arr) {
  let n = arr.length;
  for (let i = 1; i < n; i++) {
    let key = arr[i];
    let j = i - 1;
    // Move elements of arr[0..i-1] that are greater than key
    while (j >= 0 && arr[j] > key) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = key;
  }
  return arr;
}

const insertionSortedArray = insertionSort([2, 2, 2, 0, 0, 0, 1, 1]);
console.log(insertionSortedArray); // Output: [0, 0, 0, 1, 1, 2, 2, 2]

```

</p>
</details>

---

###### 4. Merge Sort

Description: Merge Sort is a divide-and-conquer algorithm that splits the array in half, sorts each half, and merges them back together.

##### Time Complexity
- Best, Average, and Worst Case: 𝑂(𝑛log𝑛)

<details>
<summary><b>Implementation</b></summary>
<p>

#### Code: 

```javascript
function mergeSort(arr) {
  if (arr.length <= 1) return arr;

  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));

  return merge(left, right);
}

function merge(left, right) {
  let result = [];
  let i = 0, j = 0;

  while (i < left.length && j < right.length) {
    if (left[i] < right[j]) {
      result.push(left[i]);
      i++;
    } else {
      result.push(right[j]);
      j++;
    }
  }

  return result.concat(left.slice(i)).concat(right.slice(j));
}

const mergeSortedArray = mergeSort([2, 2, 2, 0, 0, 0, 1, 1]);
console.log(mergeSortedArray); // Output: [0, 0, 0, 1, 1, 2, 2, 2]

```

</p>
</details>

---

###### 5. Quick Sort

Description: Quick Sort is another divide-and-conquer algorithm that selects a "pivot" element and partitions the array into elements less than and greater than the pivot, recursively sorting the partitions.

##### Time Complexity
- Best and Average Case: 𝑂(𝑛log⁡𝑛)O(nlogn)
- Worst Case:𝑂(𝑛2) (when the smallest or largest element is always chosen as the pivot)

<details>
<summary><b>Implementation</b></summary>
<p>

#### Code: 

```javascript
function quickSort(arr) {
  if (arr.length <= 1) return arr;

  const pivot = arr[arr.length - 1];
  const left = [];
  const right = [];

  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  return [...quickSort(left), pivot, ...quickSort(right)];
}

const quickSortedArray = quickSort([2, 2, 2, 0, 0, 0, 1, 1]);
console.log(quickSortedArray); // Output: [0, 0, 0, 1, 1, 2, 2, 2]

```

</p>
</details>

---

###### 6. Counting Sort

Description: Counting Sort is a non-comparison-based sorting algorithm. It counts the occurrences of each unique element in the input array and uses this information to place elements in the correct position in the output array. This algorithm is efficient when the range of input values (k) is not significantly larger than the number of elements (n).

##### Time Complexity
- Best, Average, and Worst Case: 𝑂(𝑛+𝑘), where 𝑘 is the range of the input values.

<details>
<summary><b>Implementation</b></summary>
<p>

#### Code: 

```javascript
function countingSort(arr) {
  const maxVal = Math.max(...arr);
  const count = new Array(maxVal + 1).fill(0);
  const output = new Array(arr.length);

  // Count occurrences of each element
  for (let num of arr) {
    count[num]++;
  }

  // Update the count array to reflect the position of elements
  for (let i = 1; i <= maxVal; i++) {
    count[i] += count[i - 1];
  }

  // Build the output array
  for (let i = arr.length - 1; i >= 0; i--) {
    output[count[arr[i]] - 1] = arr[i];
    count[arr[i]]--;
  }

  return output;
}

const countingSortedArray = countingSort([2, 2, 2, 0, 0, 0, 1, 1]);
console.log(countingSortedArray); // Output: [0, 0, 0, 1, 1, 2, 2, 2]

```

</p>
</details>

---


###### 7. Radix Sort

Description: Radix Sort is a non-comparison-based sorting algorithm that sorts numbers digit by digit, starting from the least significant digit to the most significant digit. It uses a stable sub-sorting algorithm, such as Counting Sort, to sort the digits.

##### Time Complexity
- Best, Average, and Worst Case: 𝑂(𝑛.𝑘), where 𝑘 is the range of digits in the largest number.

<details>
<summary><b>Implementation</b></summary>
<p>

#### Code: 

```javascript
function countingSortForRadix(arr, exp) {
  const output = new Array(arr.length);
  const count = new Array(10).fill(0);

  // Count occurrences of each digit
  for (let i = 0; i < arr.length; i++) {
    count[Math.floor(arr[i] / exp) % 10]++;
  }

  // Update the count array to reflect the position of elements
  for (let i = 1; i < count.length; i++) {
    count[i] += count[i - 1];
  }

  // Build the output array
  for (let i = arr.length - 1; i >= 0; i--) {
    output[count[Math.floor(arr[i] / exp) % 10] - 1] = arr[i];
    count[Math.floor(arr[i] / exp) % 10]--;
  }

  // Copy the output array to arr
  for (let i = 0; i < arr.length; i++) {
    arr[i] = output[i];
  }
}

function radixSort(arr) {
  // Find the maximum number to know the number of digits
  const max = Math.max(...arr);

  // Apply counting sort to sort elements based on each digit
  for (let exp = 1; Math.floor(max / exp) > 0; exp *= 10) {
    countingSortForRadix(arr, exp);
  }

  return arr;
}

const radixSortedArray = radixSort([2, 2, 2, 0, 0, 0, 1, 1]);
console.log(radixSortedArray); // Output: [0, 0, 0, 1, 1, 2, 2, 2]

```

</p>
</details>

---

#### Summary

1. Bubble Sort: Simple, inefficient for large datasets.
2. Selection Sort: Simple, but also inefficient for large datasets.
3. Insertion Sort: Efficient for small datasets or nearly sorted data.
4. Merge Sort: Efficient and stable, good for large datasets.
5. Quick Sort: Very efficient for average cases but can degrade with poor pivot choices.
6. Counting Sort: Efficient for sorting integers when the range is small compared to the number of elements.
7. Radix Sort: Efficient for sorting large sets of numbers or strings when they can be broken down into digits or characters.

#### Which Sorting Algorithm Should I Use?
It depends. Each algorithm comes with its own set of pros and cons.

<h5>Quicksort</h5> is a good default choice. It tends to be fast in practice, and with some small tweaks its dreaded O(n2) worst-case time complexity becomes very unlikely. A tried and true favorite.
<h5>Heapsort</h5> is a good choice if you can't tolerate a worst-case time complexity of O(n2) or need low space costs. The Linux kernel uses heapsort instead of quicksort for both of those reasons.
<h5>Merge sort</h5> is a good choice if you want a stable sorting algorithm. Also, merge sort can easily be extended to handle data sets that can't fit in RAM, where the bottleneck cost is reading and writing the input on disk, not comparing and swapping individual items.
<h5>Radix sort</h5> looks fast, with its O(n) worst-case time complexity. But, if you're using it to sort binary numbers, then there's a hidden constant factor that's usually 32 or 64 (depending on how many bits your numbers are). That's often way bigger than O(lg(n)), meaning radix sort tends to be slow in practice.
<h5>Counting sort</h5> is a good choice in scenarios where there are small number of distinct values to be sorted. This is pretty rare in practice, and counting sort doesn't get much use.

Each sorting algorithm has tradeoffs. You can't have it all.
