# Relative vs Absolute Paths — Git Bash Module

**For:** `rohinibarla`  ·  **Home:** `/c/Users/rohinibarla`  ·  **Practice area:** `~/Desktop`
**Tool:** Git Bash on Windows  ·  **Command:** `cd`

---

## 0. Mental model (చిన్న ఆలోచన)

In Git Bash, the very top is the **root** `/`. Your `C:` drive is `/c`, and your home folder is
`/c/Users/rohinibarla` — which Git Bash also lets you write as `~`.

Run `pwd` ("**మీరు ఎక్కడ ఉన్నారు** — where are you?") constantly. It prints your current folder.
Path-finding only makes sense once you know where you stand.

- **`.`** → ఇక్కడ (here, the current folder)
- **`..`** → పైన ఉన్న folder (the parent, one step up)
- **`<name>`** → లోపలికి (step down into a child folder)

**Postal analogy.** An *absolute* path is your **full postal address** (House 12, Gandhi Street,
Vijayawada, Andhra, Bharath) — valid no matter where you are standing. A *relative* path is
**"go up one floor, then the second door"** — only meaningful from where you currently stand.

---

## 1. Notes: Absolute vs Relative

|                       | **Absolute path**                | **Relative path**                       |
| --------------------- | -------------------------------- | --------------------------------------- |
| Starts from           | root `/`                         | your current folder (`pwd`)             |
| Begins with           | `/` (e.g. `/c/Users/...`)        | a name, or `.`, or `..`                 |
| Same from anywhere?   | **Yes** — never changes          | **No** — depends on where you stand     |
| Building blocks       | the full chain of folder names   | `.`, `..`, and child-folder names       |
| Good when             | you want one address that always works | you are moving "nearby"            |

**One-line rule:** if it starts with `/`, it's absolute. Otherwise it's relative.

---

## 2. Structure 1 — `Kutumbam` (కుటుంబం / family tree)

A family tree is the *perfect* picture for paths, because folders relate exactly like relatives:

- Same parent → **siblings** (అన్నదమ్ములు / అక్కచెల్లెళ్ళు)
- Different parents but same grandparent → **cousins**

Moving between **cousins** is where relative paths get genuinely instructive — you must climb **up**
with `..` to the common ancestor, then come back **down** the other branch.

### Build it

```bash
cd ~/Desktop
mkdir -p Kutumbam/Peddamma/Ravi
mkdir -p Kutumbam/Peddamma/Sita
mkdir -p Kutumbam/Pinni/Kiran
mkdir -p Kutumbam/Pinni/Geetha
```

### Picture it

```
Desktop/
└── Kutumbam/
    ├── Peddamma/          (పెద్దమ్మ branch)
    │   ├── Ravi/
    │   └── Sita/
    └── Pinni/             (పిన్ని branch)
        ├── Kiran/
        └── Geetha/
```

> Folder names are single ASCII words on purpose: no spaces (which would need quotes) and no
> special characters (which confuse beginners on Windows). Teach the exact capitalisation — real
> Linux servers are case-sensitive even though Windows is forgiving.

### Worked problem A — siblings (same parent)

**You are here → `Ravi`.  Go there → `Sita`.**
`pwd` shows: `/c/Users/rohinibarla/Desktop/Kutumbam/Peddamma/Ravi`

```bash
# Relative
cd ../Sita

# Absolute
cd /c/Users/rohinibarla/Desktop/Kutumbam/Peddamma/Sita
```

**Why:** Ravi and Sita share the same parent, `Peddamma`. Step up once (`..` lands you on
`Peddamma`), then step down into `Sita`. **Siblings are always just `../<name>`.**

### Worked problem B — cousins (different parents)

**You are here → `Ravi`.  Go there → `Kiran`.**

```bash
# Relative
cd ../../Pinni/Kiran

# Absolute
cd /c/Users/rohinibarla/Desktop/Kutumbam/Pinni/Kiran
```

**Why:** Ravi lives under `Peddamma`, Kiran under `Pinni` — they are cousins. Climb up **twice**
to the common grandparent `Kutumbam` (`..` → `Peddamma`, `..` → `Kutumbam`), then come back down
the other branch: `Pinni` → `Kiran`. Notice the absolute path *doesn't care* where you started —
it's the same address every time.

### Practice questions — Structure 1

1. You are in `Sita`. Go to `Geetha`. *(cousin)*
2. You are in `Kiran`. Go to `Ravi`. *(cousin, other direction)*
3. You are in `Geetha`. Go to `Kiran`. *(sibling)*
4. You are in `Ravi`. Go to the `Pinni` folder itself (the aunt, not a cousin).
5. You are in `Sita`. Go all the way back up to `Desktop`.
6. **Challenge:** From `Ravi`, reach `Geetha` with a relative path. How many `..` did you need, and which folder do they land you on?

---

## 3. Structure 2 — `Bharath` (భారత్ / geography)

Same shape, different picture: states are branches, cities are leaves. Two cities in the same state
are siblings; two cities in different states are cousins.

### Build it

```bash
cd ~/Desktop
mkdir -p Bharath/Andhra/Vijayawada
mkdir -p Bharath/Andhra/Tirupati
mkdir -p Bharath/Telangana/Hyderabad
mkdir -p Bharath/Telangana/Warangal
```

### Picture it

```
Desktop/
└── Bharath/
    ├── Andhra/            (ఆంధ్ర)
    │   ├── Vijayawada/
    │   └── Tirupati/
    └── Telangana/         (తెలంగాణ)
        ├── Hyderabad/
        └── Warangal/
```

### Practice questions — Structure 2

1. You are in `Vijayawada`. Go to `Tirupati`. *(sibling cities, same state)*
2. You are in `Vijayawada`. Go to `Hyderabad`. *(cousin — different state)*
3. You are in `Warangal`. Go to `Tirupati`. *(cousin)*
4. You are in `Hyderabad`. Go to the `Andhra` state folder.
5. You are in `Tirupati`. Go up to `Bharath` in a single command.
6. **Two-step:** You are in `Warangal`. First go to `Vijayawada`, then from there go to `Hyderabad`. Write both moves as relative paths.

---

## 4. The reusable recipe (పునరావృతం)

Once a tree exists, you can keep inventing "**here → there**" questions forever. To solve any one:

**Relative path:**
1. Find the **lowest common ancestor** of "here" and "there".
2. Count the steps up to it — that's how many `..` you need.
3. Then spell the downward path of child names to the target.

**Absolute path:**
- Always the full chain: `/c/Users/rohinibarla/Desktop/<...>` — no counting, no thinking about
  where you stand. Same answer from anywhere.

**Handy `cd` shortcuts to teach alongside:**

| Command   | Meaning                                  |
| --------- | ---------------------------------------- |
| `pwd`     | print where you are now                  |
| `cd ~`    | jump straight home (`/c/Users/rohinibarla`) |
| `cd -`    | jump back to the **previous** folder     |
| `cd ..`   | up one level                             |
| `cd`      | (alone) also goes home                   |
| `ls`      | look around before you leap              |

> **Teaching tip:** make students run `pwd` *before and after every `cd`*. Seeing the address change
> turns the abstract `..` into something they can watch happen.
