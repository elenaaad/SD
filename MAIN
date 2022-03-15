#include <iostream>
#include <vector>
#include <fstream>
#include <cstdlib>
#include <algorithm>
#include <bits/stdc++.h>

using namespace std;
using namespace std::chrono;

int generatornr() // functie care genereaza numerele
{
    int randomn, bit;
    randomn = 0;
    for(int i = 0; i < 16; i++)
    {
        bit = rand() %2;
        randomn += pow(2,i)* bit;
    }
    return randomn;
}

int test_Sort (vector<int> & v, int n)
{
    for(int i = 1; i <= n-1; i++)
        if(v[i] < v[i-1])
            return 0;
    return 1;
}

int getMax(vector<int> & v, int n)
{
    int max = v[0];
    for (int i = 1; i < n; i++)
        if (v[i] > max)
            max = v[i];
    return max;
}

void countSort(vector<int> & v, int n, int exp)
{
    int output[n];
    int i, count[10] = { 0 };


    for (i = 0; i < n; i++)
        count[(v[i] / exp) % 10]++;

    for (i = 1; i < 10; i++)
        count[i] += count[i - 1];

    for (i = n - 1; i >= 0; i--) {
        output[count[(v[i] / exp) % 10] - 1] = v[i];
        count[(v[i] / exp) % 10]--;
    }

    for (i = 0; i < n; i++)
        v[i] = output[i];
}

//NativeSort

void NativeSort (vector <int> &v, int n)
{

}

// Radix Sort
void radixsort( vector <int> &v, int n)
{
    auto start1 = high_resolution_clock::now();
    // gasim nr max ca sa aflam ordinul nr
    int m = getMax(v,  n);

    for (int exp = 1; m / exp > 0; exp *= 10)
        countSort(v, n, exp);

    auto stop1 = high_resolution_clock::now();
    auto duration1 = duration_cast<microseconds>(stop1 - start1);
    if(test_Sort(v, n) == 1)
        cout << "RadixSort: CORECT- Timp: "<<duration1.count()<<" microsecunde"<< endl;
    else
        cout << "radixsort nu a sortat bine"<<endl;
}


void merge(vector <int> & v, int low, int m, int high)
{
    int i, j, k;
    int n1 = m - low + 1;
    int n2 =  high - m;

    int *L = new int[n1], *R = new int[n2];

    for (i = 0; i < n1; i++)
        L[i] = v[low + i];
    for (j = 0; j < n2; j++)
        R[j] = v[m + 1+ j];

    i = 0;
    j = 0;
    k = low;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            v[k] = L[i];
            i++;
        }
        else
        {
            v[k] = R[j];
            j++;
        }
        k++;
    }

    while (i < n1)
    {
        v[k] = L[i];
        i++;
        k++;
    }

    while (j < n2)
    {
        v[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(vector <int> & v, int low, int high) // n = 10^7 maxx = 10^8
{
    if (low < high)
    {
        long long m = low+(high-low)/2;

        mergeSort(v, low, m);
        mergeSort(v, m+1, high);

        merge(v, low, m, high);
    }
}

// Shell sort
void shellSort(int n, vector <int> & v)
{

    // Rearanjam elem la fiecare n/2, n/4, n/8...
    for (int interval = n / 2; interval > 0; interval /= 2) {
        for (int i = interval; i < n; i += 1) {
            int temp = v[i];
            int j;
            for (j = i; j >= interval && v[j - interval] > temp; j -= interval) {
                v[j] = v[j - interval];
            }
            v[j] = temp;
        }
    }
}

void bubblesort(int n, vector<int> & v)
{
    auto start = high_resolution_clock::now();
    int i, ok;
    do
    {
        ok = 1;
        for(i = 0; i < n; i++)
            if(v[i] > v[i+1])
            {
                //swap
                v[i] += v[i+1];
                v[i+1] = v[i] - v[i+1];
                v[i] -= v[i+1];
                ok = 0;
            }
    }
    while(ok == 0);

    auto stop = high_resolution_clock::now();
    auto duration = duration_cast<microseconds>(stop - start);
    if(test_Sort(v, n) == 1)
        cout << "Bubblesort: CORECT- Timp: "<<duration.count()<<" microsecunde "<<'\n';
    else
        cout << "Bubblesort nu a sortat bine"<<endl;
}

int mediana(int left, int right, vector <int> &v)
{
    int x,y,z,i,j;
    x = v[left];
    y = v[(right-left)/2+left];
    z = v[right-1];
    i = left-1;
    j = right;

    if(y>x && y<z || y>z && y<x)
        x=y;
    else if(z>x && z<y || z>y && z<x)
        x=z;

    while(1){
        do {
            j--;
        }while(v[j]>x);

        do {
            i++;
        }while(v[i]<x);

        if (i<j) swap(v[i],v[j]);
        else return j+1;

    }

}
void quicksort(int p, int u, vector<int> &v)
{
    int pv;
    if (u - p >= 2) {
        pv = mediana(p, u, v);

        quicksort(p, pv, v);
        quicksort(pv, u, v);
    }
}

int main()
{
    ifstream f("intrare.txt");
    int n, Mx, x, N;

    f>>N;
    for (int k=1;k<=N;k++)
        {
        f>>n>>Mx;
        vector<int> v,c; //vector cu N numere generate random
        srand(time(NULL));
        v.push_back(Mx);
        for (int i = 1; i < n; i++){
            x = generatornr();
            if (x <= Mx && x >= 0)

                v.push_back(x);

            else
                i--;
        }
        cout<<endl;


        if(n > 100000000)
            cout<<"NativeSort: Nu exista suficienta memorie vector";
                else
            { c.clear();
                for (int j = 0; j < n; j++)
                    c.push_back(v[j]);

                auto start = high_resolution_clock::now();
                sort(c.begin(), c.end());
                auto stop = high_resolution_clock::now();
                auto duration = duration_cast<microseconds>(stop - start);
                if(test_Sort(c, n) == 1)
                    cout << "NativeSort: CORECT- Timp: " << duration.count() << " microsecunde" << endl;
                else
                    cout << "NativeSort nu a sortat bine"<<endl;
            }


        if (n > 100000000)
            cout << "RadixSort: Nu exista suficienta memorie pentru vector" << endl;
        else
        {
            c.clear();
        for (int j = 0; j < n; j++)
                c.push_back(v[j]);
            radixsort(c, n - 1);
        }


        if (n > 10000000)
            cout << "MergeSort: Nu exista suficienta memorie pentru vector" << endl;
        else
        {
            c.clear();
            for (int j = 0; j < n; j++)
                c.push_back(v[j]);
            auto start = high_resolution_clock::now();
            mergeSort(c, 0, n - 1);
            auto stop = high_resolution_clock::now();
            auto duration = duration_cast<microseconds>(stop - start);
            if (test_Sort(c, n) == 1)
                cout << "MergeSort: CORECT- Timp: " << duration.count()
                     << " microsecunde"
                     << endl;
            else cout << "MergeSort nu a sortat bine\n";
        }




        if (n > 10000000)
            cout << "ShellSort: Nu exista suficienta memorie pentru vector" << endl;
        else
        {
            c.clear();
            for (int j = 0; j < n; j++)
                c.push_back(v[j]);
            auto start = high_resolution_clock::now();
            shellSort(n, c);
            auto stop = high_resolution_clock::now();
            auto duration = duration_cast<microseconds>(stop - start);
            if (test_Sort(c, n) == 1)
                cout << "ShellSort: CORECT- Timp: " << duration.count()
                     << " microsecunde"
                     << endl;
            else cout << "ShellSort nu a sortat bine\n";
        }

        if (n > 10000)
            cout << "BubbleSort: Nu exista suficienta memorie pentru vector" << endl;
        else
        {
            c.clear();
            for (int j = 0; j < n; j++)
                c.push_back(v[j]);
            bubblesort(n, v);
        }


        if(n > 100000000)
            cout<<"QuickSort mediana: Nu exista suficienta memorie pentru vector"<<endl;
        else
        { c.clear();
            for (int j = 0; j < n; j++)
                c.push_back(v[j]);
            auto start = high_resolution_clock::now();
            quicksort(0, n, c);
            auto stop = high_resolution_clock::now();
            auto duration = duration_cast<microseconds>(stop - start);
            if(test_Sort(c,n)==1)
                cout<<"QuickSort mediana: CORECT- Timp: "<<duration.count() <<" microsecunde"<< endl;
            else cout<<"Quicksort mediana nu a sortat bine";
        }

        c.clear();
        v.clear();

    }

    return 0;
}
