# 🎮 Enemy AI FSM - Unity Project

## 📌 Deskripsi

Project ini merupakan implementasi **Finite State Machine (FSM)** pada Enemy AI di Unity.
Enemy memiliki beberapa state utama yaitu **Idle**, **Chase**, dan **Attack**, yang memungkinkan perilaku berubah secara dinamis berdasarkan jarak terhadap player.

---

## 🧠 Konsep yang Digunakan

* Finite State Machine (FSM)
* Scriptable Object sebagai State
* State Transition berbasis kondisi (jarak ke player)
* Movement menggunakan Rigidbody2D

---

## ⚙️ State Behavior

### 🟢 Idle State

* Enemy diam (tidak bergerak)
* Akan berpindah ke **Chase State** jika player masuk ke dalam `chaseRange`

---

### 🟡 Chase State

* Enemy bergerak mendekati player
* Menggunakan `Vector2.MoveTowards`
* Transisi:

  * ➡️ ke **Attack State** jika jarak < `attackRange`
  * ⬅️ kembali ke **Idle State** jika jarak > `chaseRange`

---

### 🔴 Attack State

* Enemy melakukan aksi menyerang (log/debug)
* Akan kembali ke **Chase State** jika player keluar dari `attackRange`

---

## 🧩 Struktur Script

### `EnemyController.cs`

Mengatur:

* State aktif
* Perpindahan state (`ChangeState`)
* Referensi player
* Parameter seperti:

  * `speed`
  * `chaseRange`
  * `attackRange`

---

### `StateSO.cs`

Abstract class untuk semua state:

```csharp
public abstract void Enter(EnemyController enemy);
public abstract void Execute(EnemyController enemy);
public abstract void Exit(EnemyController enemy);
```

---

### State Implementation

* `IdleStateSO.cs`
* `ChaseStateSO.cs`
* `AttackStateSO.cs`

Semua state dibuat menggunakan **ScriptableObject** agar modular dan reusable.

---
