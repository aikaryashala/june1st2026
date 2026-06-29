# Answer Key — Relative vs Absolute Paths

Companion to `relative-vs-absolute-paths.md`. Every move is solved both ways.

---

## Structure 1 — `Kutumbam`

```
Desktop/Kutumbam/
├── Peddamma/{Ravi, Sita}
└── Pinni/{Kiran, Geetha}
```

| # | Move (here → there) | Relative | Absolute |
|---|----------------------|----------|----------|
| 1 | Sita → Geetha *(cousin)* | `cd ../../Pinni/Geetha` | `cd /c/Users/rohinibarla/Desktop/Kutumbam/Pinni/Geetha` |
| 2 | Kiran → Ravi *(cousin)* | `cd ../../Peddamma/Ravi` | `cd /c/Users/rohinibarla/Desktop/Kutumbam/Peddamma/Ravi` |
| 3 | Geetha → Kiran *(sibling)* | `cd ../Kiran` | `cd /c/Users/rohinibarla/Desktop/Kutumbam/Pinni/Kiran` |
| 4 | Ravi → Pinni *(the aunt)* | `cd ../../Pinni` | `cd /c/Users/rohinibarla/Desktop/Kutumbam/Pinni` |
| 5 | Sita → Desktop | `cd ../../..` | `cd /c/Users/rohinibarla/Desktop`  (or `cd ~/Desktop`) |
| 6 | Ravi → Geetha *(challenge)* | `cd ../../Pinni/Geetha` | `cd /c/Users/rohinibarla/Desktop/Kutumbam/Pinni/Geetha` |

**Q6 explanation:** two `..` are needed. The first lands on `Peddamma`, the second on `Kutumbam`
(the common grandparent). From there, descend the other branch: `Pinni/Geetha`.

---

## Structure 2 — `Bharath`

```
Desktop/Bharath/
├── Andhra/{Vijayawada, Tirupati}
└── Telangana/{Hyderabad, Warangal}
```

| # | Move (here → there) | Relative | Absolute |
|---|----------------------|----------|----------|
| 1 | Vijayawada → Tirupati *(sibling)* | `cd ../Tirupati` | `cd /c/Users/rohinibarla/Desktop/Bharath/Andhra/Tirupati` |
| 2 | Vijayawada → Hyderabad *(cousin)* | `cd ../../Telangana/Hyderabad` | `cd /c/Users/rohinibarla/Desktop/Bharath/Telangana/Hyderabad` |
| 3 | Warangal → Tirupati *(cousin)* | `cd ../../Andhra/Tirupati` | `cd /c/Users/rohinibarla/Desktop/Bharath/Andhra/Tirupati` |
| 4 | Hyderabad → Andhra *(state folder)* | `cd ../../Andhra` | `cd /c/Users/rohinibarla/Desktop/Bharath/Andhra` |
| 5 | Tirupati → Bharath | `cd ../..` | `cd /c/Users/rohinibarla/Desktop/Bharath` |
| 6 | Warangal → Vijayawada → Hyderabad *(two-step)* | `cd ../../Andhra/Vijayawada` then `cd ../../Telangana/Hyderabad` | — |

**Q6 explanation:** each leg climbs two levels to `Bharath`, then descends into the target state and
city. After the first leg you are *standing in* `Vijayawada`, so the second leg's `..` count is
measured from there — a good reminder that relative paths always restart from `pwd`.
