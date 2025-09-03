#include <stdio.h>
#include <stdlib.h>

float totalSale(float sales[], int n) {
    float total = 0.0;
    for (int i = 0; i < n; i++) {
        total += sales[i];
    }
    return total;
}

float maxSale(float sales[], int n) {
    float max = sales[0];
    for (int i = 1; i < n; i++) {
        if (sales[i] > max) {
            max = sales[i];
        }
    }
    return max;
}

int main() {
    FILE *fp;
    int count = 0;
    float value;

    fp = fopen("sales.txt", "r");
    if (fp == NULL) {
        perror("Open file failed");
        return 1;
    }

    while (fscanf(fp, "%f", &value) == 1) {
        count++;
    }

    rewind(fp);

    float *sales = (float *)malloc(count * sizeof(float));
    if (sales == NULL) {
        perror("Memory failed");
        fclose(fp);
        return 1;
    }

    for (int i = 0; i < count; i++) {
        fscanf(fp, "%f", &sales[i]);
    }

    float total = totalSale(sales, count);
    float max = maxSale(sales, count);

    printf("Total sales: %.2f\n", total);
    printf("Maximum sale: %.2f\n", max);
    fclose(fp);

    return 0;
}
