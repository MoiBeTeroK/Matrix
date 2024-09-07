#include <iostream>
using namespace std;

void print(float** a, int n) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << a[i][j] << "\t";
        }
        cout << endl;
    }
}
float diag(float** a, int n) {
    float k = 0;
    for (int i = 0; i < n; i++) {
        k += a[i][i];
    }
    return k;
}
float** sum(float** a, float** b, int n) {
    float** c;
    c = new float* [n];
    for (int i = 0; i < n; i++) {
        c[i] = new float[n];
    }
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            c[i][j] = a[i][j] + b[i][j];
        }
    }
    return c;
}
float** mul(float** a, float** b, int n) {
    float** c;
    c = new float* [n];
    for (int i = 0; i < n; i++) {
        c[i] = new float[n];
    }
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            c[i][j] = 0;
            for (int k = 0; k < n; k++)
                c[i][j] += a[i][k] * b[k][j];
        }
    }
    return c;
}

float** single(int n) {
    float** c;
    c = new float* [n];
    for (int i = 0; i < n; i++) {
        c[i] = new float[n];
        for (int j = 0; j < n; j++) {
            if (i == j) c[i][j] = 1;
            else c[i][j] = 0;
        }
    }
    return c;
}

float** mulNum(float** a, float x, int n) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            a[i][j] *= x;
        }
    }
    return a;
}

float* f(float** A, int n) {
    float* C = new float[n + 1];
    auto I = single(n);
    C[n] = 1;

    auto M = single(n);
    for (int i = 0; i < n; i++)
        M[i][i] = 0;

    for (int k = 1; k <= n; k++)
    {
        M = sum(mul(A, M, n), mulNum(I, C[n - k + 1], n), n);
        C[n - k] = -diag(mul(A, M, n), n) / k;

        for (int i = 0; i < n; i++)
            I[i][i] = 1;
    }

    for (int i = 0; i < n; i++) {
        delete M[i];
        delete I[i];
    }
    delete[] M;
    delete[] I;

    return C;
}

void poly(float* c, int n) {
    cout << "P(x) = ";
    for (int i = n; i >= 0; i--) {
        if (i == 0) cout << " " << c[i];
        else if (c[i] < 0) cout << " " << c[i] << "x^" << i;
        else if (c[i] > 0 && i!=n) cout << " + " << c[i] << "x^" << i;
        else if (c[i] > 0 && i == n) cout << c[i] << "x^" << i;
        else if (c[i] == 0) continue;
    }
}

int main() {
    setlocale(LC_ALL, "rus");
    int n; 
    cout << "Введите размерность матрицы: ";
    cin >> n;
    float** a;
    a = new float* [n];
    for (int i = 0; i < n; i++) {
        a[i] = new float[n];
    }
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << "a[" << i << "][" << j << "]= ";
            cin >> a[i][j];
        }
    }
    cout << endl;
    print(a, n);
    cout << endl;
    float* b = f(a, n);
    poly(b, n);
    cout << endl;
    for (int i = 0; i < n; i++) {
        delete a[i];
    }
    delete[]a;
    delete b;

}
