---
layout: post
title:  "Algorithm - Sort Functions"
date:   2019-12-20 21:03:36 +0530
tags: "algorithm sort"
---

Sort Functions là bài đầu tiên trong loạt bài viết về thuật toán cơ bản nhằm ôn lại kiến thức nền tảng.

## 1. Selection Sort
Độ phức tạp trung bình O(n^2)
```c
void SelectionSort(int *A, int n)
	{
		for (int i = 0; i < n; i++)
		{
			for (int j = i; j < n; j++)
			{
				if (A[i] > A[j])
				{
					int temp = A[i];
					A[i] = A[j];
					A[j] = temp;
				}
			}
		}
	}
```

## 2. Bubble Sort
Độ phức tạp trung bình O(n^2)
```c
void BubbleSort(int *A, int n)
	{
		for (int i = n; i > 0; i--)
		{
			for (int j = 0; j < i-1; j++)
			{
				if (A[j] > A[j + 1])
				{
					int temp = A[j + 1];
					A[j + 1] = A[j];
					A[j] = temp;
				}
			}
		}
	}
```

## 3. Quick Sort
Độ phức tạp trung bình là O(nlog(n)) và là tệ nhất O(n^2). Quicksort is a divide and conquer algorithm.
```c
int Partition(int A[], int lo, int hi)
	{
		int pivot = lo;
		int i = lo;
		int j = hi;
		while (true)
		{
			while (A[i] <= A[pivot] && i < hi)
			{
				i++;
			}

			while (A[j] >= A[pivot] && j > lo)
			{
				j--;
			}

			if (i >= j)
			{
				int temp = A[j];
				A[j] = A[pivot];
				A[pivot] = temp;
				return j;
			}
			else
			{
				int temp = A[j];
				A[j] = A[i];
				A[i] = temp;
			}
		}
	}

	void QuickSort(int A[], int lo, int hi)
	{
		if (lo < hi)
		{
			int pivot = Partition(A, lo, hi);
			QuickSort(A, lo, pivot - 1);
			QuickSort(A, pivot + 1, hi);
		}
	}
```
## 4. Merge Sort
Độ phức tạp trung bình O(n)log(n), Usually done recursively, divide and conquer.
```c
void Merge(int A[], int first, int middle, int last)
	{
		int *tempArr = new int[last - first + 1];
		int first1 = first;
		int last1 = middle;
		int first2 = middle + 1;
		int last2 = last;
		int index = 0;

		while ((first1 <= last1) && (first2 <= last2))
			if (A[first1] <= A[first2])
				tempArr[index++] = A[first1++];
			else
				tempArr[index++] = A[first2++];

		if (first1 > last1)
			while (first2 <= last2)
				tempArr[index++] = A[first2++];

		if (first2 > last2)
			while (first1 <= last1)
				tempArr[index++] = A[first1++];

		for (int i = 0; i < index; i++)
			A[first + i] = tempArr[i];

		delete[] tempArr;
	}

	void MergeSort(int A[], int first, int last)
	{
		if (first < last)
		{
			int mid = (first + last) / 2;
			MergeSort(A, first, mid);
			MergeSort(A, mid + 1, last);
			Merge(A, first, mid, last);
		}
	}
```

## 5. Heap Sort

## 6. Demo
```c
void Run()
{
    ifstream readFile;
    readFile.open("input_data.txt");
    int n;
    int A[1000];
    readFile >> n;
    for (int i = 0; i < n; i++)
    {
        readFile >> A[i];
        cout << A[i] << "\t";
    }

    QuickSort(A, n);

    cout << endl;
    for (int i = 0; i < n; i++)
    {
        cout << A[i] << "\t";
    }
    readFile.close();
}

```