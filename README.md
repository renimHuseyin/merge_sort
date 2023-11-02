//merge_sort
//merge sort sıralama algoritması kullanılarak rastgele sayılarla oluşturulan diziyi sıralama
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <time.h>

// İki alt diziyi birleştiren fonksiyon
void merge(int arr[], int l, int m, int r) {
    int i, j, k;
    int n1 = m - l + 1;
    int n2 = r - m;

    // Geçici diziler oluşturulur
    int L[n1], R[n2];

    // Geçici dizilere veriler kopyalanır
    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    // İki alt dizi birleştirilir
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    // Geriye kalan elemanlar kopyalanır
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// Merge Sort'u uygulayan fonksiyon
void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2; // Orta nokta hesaplanır

        // İlk yarıyı sırala
        mergeSort(arr, l, m);

        // İkinci yarıyı sırala
        mergeSort(arr, m + 1, r);

        // İki yarıyı birleştir
        merge(arr, l, m, r);
    }
}

int main() {
    //int arr[] = {12, 11, 13, 5, 6, 7};
    srand(time(NULL));
	int girilen_sayi_adedi=100;
    int arr[100] = {0};
    int n = sizeof(arr) / sizeof(arr[0]); //dizi boyutunun hesaplanması
    int i;
    
    for(i=0; i<girilen_sayi_adedi;i++)
    {
    	arr[i] = rand()%girilen_sayi_adedi+1;
	}

    printf("Siralanmamis dizi: \n");
    for (i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    mergeSort(arr, 0, n - 1);

    printf("Siralanmis dizi: \n");
    for (i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }

    return 0;
}
