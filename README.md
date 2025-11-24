# Zadání – Získávání systémových informací v Bash pomocí sed a awk

Vaším úkolem je vytvořit bash skript, který získá základní informace o systému pomocí standardních Linux příkazů a zpracuje jejich výstup pomocí **sed** a **awk**.
V kodu vhodně vytvořte funkce tak, aby jste mohli snadno získávat každou hodnotu dle zadání. Ne nutně však musí mít každá hodnota svou vlastní metodu viz ukázka níže.
```bash
#funkce k získání vytížení CPU
get_cpu_usage {
# todo
}

#funkce pro výpis RAM paměti
# 1. sloupec total;
# 2. sloupec free;
# 3. sloupec used
get_ram {
# todo 
}

cpu_usage=$get_cpu_usage
free_ram=${get_ram | awk `{print $2}`}

```

---

## 1. CPU – celkové vytížení
Použijte:

```
top -b -n 1
```
<img width="1668" height="1548" alt="image" src="https://github.com/user-attachments/assets/589a13c9-52ba-4d47-8d53-08901b75ad25" />


Z řádku:

```
%Cpu(s):  7.6 us,  1.0 sy,  0.0 ni, 91.0 id, ...
```

Vyhledejte hodnotu **idle** a vypočítejte:

```
CPU: X%
```

Kde:

```
X = 100 - idle
```

---

## 2. RAM – obsazená paměť
Z výstupu `top` najděte řádek začínající:

```
MiB Mem:
```
nebo
```
KiB Mem:
```

Získejte hodnotu **used** a vypište:

```
RAM-used: Y MB
```

---

## 3. Tasks – počet procesů
Z řádku:

```
Tasks: 189 total, ...
```

Vyberte:

```
Tasks: 189
```

---

## 4. Počet jader CPU
Použijte:

```
cat /proc/cpuinfo
```

Spočítejte počet řádků začínajících:

```
processor   : 
```

Výstup:

```
Cores: N
```

---

## 5. Kapacita disku pro /dev/sda1
Použijte:

```
df /dev/sda1
```

Získejte celkovou kapacitu disku v **MB** a vypište:

```
Disk /dev/sda1: Z MB
```

---

## 6. Očekávaný výstup skriptu
Skript by měl vypsat přesně:

```
CPU: 12.5%
RAM-used: 1250MB
Tasks: 189
Cores: 4
Disk /dev/sda1: 102400MB
```

Použijte pouze příkazy: `top`, `df`, `cat /proc/cpuinfo`, `sed`, `awk`, a `grep`.
