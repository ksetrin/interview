## Сортировка пузырьком.
Сложность: `O(n²)`
const bubbleSort = arr => {
    for (let i = 0, endI = arr.length - 1; i < endI; i++) {
        for (let j = 0, endJ = endI - i; j < endJ; j++) {
            if (arr[j] > arr[j + 1]) {
                [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
            }
        }
    }
    return arr;
};

## Гномья сортировка (Gnome sort)
Сложность: `O(n²)`
const gnomeSort = arr => {
    const l = arr.length;
    let i = 1;
    while (i < l) {
        if (i > 0 && arr[i - 1] > arr[i]) {
            [arr[i], arr[i - 1]] = [arr[i - 1], arr[i]];
            i--;
        } else {
            i++;
        }
    }
    return arr;
};

## Сортировка вставками (Insertion sort)
Сложность: `O(n²)`
const insertionSort = arr => {
    for (let i = 1, l = arr.length; i < l; i++) {
        const current = arr[i];
        let j = i;
        while (j > 0 && arr[j - 1] > current) {
            arr[j] = arr[j - 1];
            j--;
        }
        arr[j] = current;
    }
    return arr;
};


## сортировка перемешиванием (Cocktail sort)
## сортировка кучей (Heapsort)
## быстрая сортировка (Quicksort)