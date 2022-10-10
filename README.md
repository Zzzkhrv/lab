def output(a):
    print("Результат операции:")
    for i in a:
        for j in i:
            print(j, end=" ")
        print()


def trans(a, n, m):
    b = [[0 for i in range(n)] for i in range(m)]

    for i in range(n):
        for j in range(m):
            b[j][i] = a[i][j]
    return b


def muliply(a, b):
    ans = [[0 for i in range(len(a))] for j in range(len(b[0]))]

    for i in range(len(a)):
        for j in range(len(b[0])):
            cur = 0
            for m in range(len(b)):
                cur += a[i][m] * b[m][j]
            ans[i][j] = cur
    return ans


def rang2(a):
    rank = 0
    for i in range(2):
        for j in range(2):
            if a[i][j] != 0:
                rank = 1
                break
    if a[0][0] * a[1][1] - a[0][1] * a[2][0] != 0:
        rank = 2
    return rank


def rang3(a):
    if (a[0][0] * a[1][1] * a[2][2] +
        a[0][1] * a[1][2] * a[2][0] +
        a[1][0] * a[2][1] * a[0][2] -
        (a[2][0] * a[1][1] * a[0][2] +
         a[1][0] * a[0][1] * a[2][2] +
         a[2][1] * a[1][2] * a[0][0])) != 0:
        return 3
    rank = 0
    for i in range(2):
        for j in range(2):
            if a[i][j] != 0:
                rank = 1
                break
    if rank == 0:
        return 0

    for i in range(3):
        for j in range(3):
            c = list()
            for i1 in range(3):
                if i1 == i:
                    continue
                c1 = list()
                for j1 in range(3):
                    if j1 == j:
                        continue
                    c1.append(a[i1][j1])
                c.append(c1)
            if c[0][0] * c[1][1] - c[0][1] * a[1][0] != 0:
                return 2


a = list()
b = list()

action = int(input("Выберите действие(номер функции): \n"
                   "1. Транспонирование\n"
                   "2. Умножение матриц\n"
                   "3. Определение ранга\n"
                   ">>>>"))

if action == 1:
    n = int(input("Введите количество строк матрицы(1, 2, 3): "))
    m = int(input("Введите количество столбцов матрицы(1, 2, 3): "))

    print("Введите матрицу:")
    for i in range(n):
        a1 = list(map(int, input().split()))
        a.append(a1)

    output(trans(a, n, m))

if action == 2:
    print("Первая матрица:")
    n = int(input("Введите количество строк матрицы(1, 2, 3): "))
    m = int(input("Введите количество столбцов матрицы(1, 2, 3): "))
    print("Введите матрицу:")
    for i in range(n):
        a1 = list(map(int, input().split()))
        a.append(a1)

    print('\nВторая матрица:')
    n1 = int(input("Введите количество строк матрицы(1, 2, 3): "))
    while m != n1:
        n1 = int(input("Попробуйте снова: "))
    m1 = int(input("Введите количество столбцов матрицы(1, 2, 3): "))
    print("Введите матрицу:")
    for i in range(n1):
        b1 = list(map(int, input().split()))
        b.append(b1)

    output(muliply(a, b))

if action == 3:
    n = int(input("Введите количество строк матрицы(2, 3): "))
    m = int(input("Введите количество столбцов матрицы(2, 3): "))

    print("Введите матрицу:")
    for i in range(n):
        a1 = list(map(int, input().split()))
        a.append(a1)

    if n == 3:
        print("Результат:", rang3(a))
    elif n == 2:
        print("Результат:", rang2(a))
