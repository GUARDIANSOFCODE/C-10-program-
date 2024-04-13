# C-10-program-
WAP to implement merge sort
#include <stdio.h>

void merge(int arr[], int l, int m, int r) {
  int n1 = m - l + 1;
  int n2 = r - m;

  // Create temporary arrays
  int left[n1], right[n2];

  // Copy data to temporary arrays
  for (int i = 0; i < n1; i++) {
    left[i] = arr[l + i];
  }
  for (int j = 0; j < n2; j++) {
    right[j] = arr[m + 1 + j];
  }

  // Merge the temporary arrays back into arr[l..r]
  int i = 0, j = 0, k = l;
  while (i < n1 && j < n2) {
    if (left[i] <= right[j]) {
      arr[k] = left[i];
      i++;
    } else {
      arr[k] = right[j];
      j++;
    }
    k++;
  }

  // Copy the remaining elements of left[]
  while (i < n1) {
    arr[k] = left[i];
    i++;
    k++;
  }

  // Copy the remaining elements of right[]
  while (j < n2) {
    arr[k] = right[j];
    j++;
    k++;
  }
}

void mergeSort(int arr[], int l, int r) {
  if (l < r) {
    // Same as (l+r)/2, but avoids overflow for large l and r
    int m = l + (r - l) / 2;

    mergeSort(arr, l, m);
    mergeSort(arr, m + 1, r);

    merge(arr, l, m, r);
  }
}

void printArray(int arr[], int n) {
  for (int i = 0; i < n; ++i) {
    printf("%d ", arr[i]);
  }
  printf("\n");
}

int main() {
  int arr[] = {6, 5, 3, 1, 8, 7, 2, 4};
  int n = sizeof(arr) / sizeof(arr[0]);

  printf("Unsorted array: \n");
  printArray(arr, n);

  mergeSort(arr, 0, n - 1);

  printf("Sorted array: \n");
  printArray(arr, n);

  return 0;
}
