# Python_tasks_2025

import requests
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

def get_monthly_avg_temp(lat, lon, timezone):
    url = (
        f"https://archive-api.open-meteo.com/v1/archive?"
        f"latitude={lat}&longitude={lon}"
        f"&start_date=2023-01-01&end_date=2023-12-31"
        f"&daily=temperature_2m_mean&timezone={timezone}"
    )
    response = requests.get(url)
    data = response.json()

    df = pd.DataFrame({
        'date': data['daily']['time'],
        'temp': data['daily']['temperature_2m_mean']
    })
    df['date'] = pd.to_datetime(df['date'])
    df['month'] = df['date'].dt.month
    monthly_avg = df.groupby('month')['temp'].mean().round(1)
    return monthly_avg.values

# Получение данных
warszawa = get_monthly_avg_temp(52.2298, 21.0118, "Europe/Warsaw")
londyn = get_monthly_avg_temp(51.5072, -0.1276, "Europe/London")
months = np.arange(1, 13)

# Построение графиков
fig, axs = plt.subplots(3, 1, figsize=(10, 15))

# 1. Линейный график
axs[0].plot(months, warszawa, marker='o', label='Warszawa', color='blue')
axs[0].plot(months, londyn, marker='s', label='Londyn', color='green')
axs[0].set_title('Średnie miesięczne temperatury (2023)')
axs[0].set_xticks(months)
axs[0].legend()
axs[0].grid(True)

# 2. Столбчатый график разницы температур
diff = londyn - warszawa
colors = ['red' if d > 0 else 'blue' for d in diff]
axs[1].bar(months, diff, color=colors)
axs[1].set_title('Różnica temperatur (Londyn - Warszawa)')
axs[1].axhline(0, color='black')
axs[1].set_xticks(months)
axs[1].grid(True)

# 3. Точечный график сравнения
sc = axs[2].scatter(warszawa, londyn, c=diff, cmap='coolwarm', s=100)
for i, (wx, lx) in enumerate(zip(warszawa, londyn)):
    axs[2].annotate(str(i+1), (wx, lx), textcoords="offset points", xytext=(5, 5), ha='center')
axs[2].plot([min(warszawa), max(warszawa)], [min(warszawa), max(warszawa)], 'k--', label='y = x')
axs[2].set_xlabel('Temperatura w Warszawie')
axs[2].set_ylabel('Temperatura w Londynie')
axs[2].set_title('Porównanie temperatur')
plt.colorbar(sc, ax=axs[2], label='Różnica (Londyn - Warszawa)')
axs[2].legend()
axs[2].grid(True)

# Сохраняем
plt.tight_layout()
plt.savefig("temperatury_2023.png")
plt.show()
-------------------------------------------------------------

import matplotlib.pyplot as plt
import numpy as np

# Średnie miesięczne temperatury (fikcyjne dane)
warszawa = np.array([-1, 0, 5, 10, 15, 19, 21, 20, 15, 10, 5, 0])
londyn = np.array([4, 5, 8, 12, 16, 19, 22, 21, 17, 13, 8, 5])
months = np.arange(1, 13)

# 1. Wykres liniowy
plt.figure(figsize=(10, 12))

plt.subplot(3, 1, 1)
plt.plot(months, warszawa, marker='o', color='blue', label='Warszawa')
plt.plot(months, londyn, marker='s', color='green', label='Londyn')
plt.title('Średnie miesięczne temperatury w 2023 roku')
plt.xticks(months)
plt.ylabel('Temperatura (°C)')
plt.legend()

# 2. Wykres słupkowy różnicy (Londyn - Warszawa)
plt.subplot(3, 1, 2)
diff = londyn - warszawa
colors = ['red' if d > 0 else 'blue' for d in diff]
plt.bar(months, diff, color=colors)
plt.title('Różnica temperatur (Londyn - Warszawa)')
plt.xticks(months)
plt.ylabel('Różnica (°C)')

# 3. Wykres punktowy: X - Warszawa, Y - Londyn
plt.subplot(3, 1, 3)
sc = plt.scatter(warszawa, londyn, c=diff, cmap='coolwarm', s=100)
for i, (x, y) in enumerate(zip(warszawa, londyn)):
    plt.text(x + 0.3, y, str(i + 1))
plt.plot(warszawa, warszawa, linestyle='--', color='black', label='y=x')
plt.colorbar(sc, label='Londyn - Warszawa')
plt.title('Temperatura Londyn vs Warszawa')
plt.xlabel('Warszawa (°C)')
plt.ylabel('Londyn (°C)')
plt.legend()

plt.tight_layout()
plt.savefig("temperatury_2023.png")
plt.show()

------------------------------------------------------

plt.plot(x, y) — линия.

plt.scatter(x, y) — точечный график.

plt.bar(x, y) — столбчатый график.

plt.hist(data) — гистограмма.

plt.title("Tytuł") — заголовок.

plt.xlabel("X"), plt.ylabel("Y") — подписи осей.

plt.legend() — легенда.

plt.grid(True) — сетка.

plt.show() — отобразить график.

plt.savefig("nazwa.png") — сохранить изображение.




np.array([1, 2, 3]) — создание массива.

np.arange(1, 13) — массив [1, 2, ..., 12].

np.mean(a) — среднее.

np.max(a), np.min(a) — максимум/минимум.

np.round(a, 1) — округление до 1 знака.

a.shape — размер массива.

a + b, a * 2 — операции над массивами.





pd.read_csv("file.csv") — чтение CSV-файла.

df.head() — первые строки.

df.info() — информация о таблице.

df.describe() — статистика.

df['kolumna'] — доступ к колонке.

df['nowa'] = ... — добавление новой колонки.

df.groupby('kolumna').mean() — группировка и среднее.

df.plot() — быстрый график.


