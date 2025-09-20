Row Wise Traversal
```java
for (int i = 0; i < n; ++i) {       // Traverse each row (i from 0 to n-1)
    for (int j = 0; j < m; ++j) {   // Traverse each column (j from 0 to m-1)
        // matrix[i][j] is the current element
    }
}
```

Column Wise Traversal
```java
for (int j = 0; j < m; ++j) {       // Traverse each column (j from 0 to m-1)
    for (int i = 0; i < n; ++i) {   // Traverse each row (i from 0 to n-1)
        // matrix[i][j] is the current element
    }
}
```

Sub-Matrix Traversal
```java
for (int x = i; x < i + k; ++x) {       // Traverse the sub-matrix rows
    for (int y = j; y < j + k; ++y) {   // Traverse the sub-matrix columns
        // matrix[x][y] is the current element of the sub-matrix
    }
}
```

Sudoku
```java
int startRow = (i / 3) * 3;  // Calculate the starting row of the sub-box
int startCol = (j / 3) * 3;  // Calculate the starting column of the sub-box

for (int x = startRow; x < startRow + 3; ++x) {    // Traverse rows in the sub-box
    for (int y = startCol; y < startCol + 3; ++y) {  // Traverse columns in the sub-box
        // matrix[x][y] is the current element in the sub-box
    }
}

```

Diagonal Traversal
```java
for (int i = 0; i < n; ++i) {  // Traverse main diagonal (i = j)
    // matrix[i][i] is the current element
}
```

Anti-Diagonal Traversal
```java
for (int i = 0; i < n; ++i) {
    // matrix[i][n - i - 1] is the current element
}
```

### **Important General Matrix Formulas**

#### 1. **Index Calculation for Sub-matrix**:

For a matrix of size n×m, the index of a sub-matrix or block is calculated as:

- Row index of sub-matrix = i / k
- Column index of sub-matrix = j / k

Where k is the size of the sub-matrix (such as 3 for a 3x3 Sudoku box).

#### 2. **1D to 2D Index Mapping** (For Flattened Matrix):

If a 2D matrix is stored in a 1D array, the 2D index (i ,j) can be mapped as
```java
index = i * m + j;  // For a row-major flattened array
m = no of columns
```
