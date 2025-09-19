

# Subdomain Enumeration – hackerone.com

**Target:** Hackerone.com 
<br>

This is the **second target** in my Subdomain Enumeration task. I followed the same process as Target 1 (Subfinder → Assetfinder → AlterX → dnsx) but applied it to `hackerone.com`.

---

## 1. Subfinder

**Command Used:**

```bash
subfinder -d hackerone.com -o subfinder.txt
```


**Screenshot:**

<p align="center">
  <img src="https://github.com/DOLLY1552005/SKill_Horizon_Internship/blob/main/Subdomain_Enumeration/screenshots/subfinder02.png" width="80%">
</p>

**Notes:**

* Discovered main subdomains like `api.hackerone.com`, `docs.hackerone.com`.
* This gave me the initial baseline for further enumeration.

---

## 2. Assetfinder

**Command Used:**

```bash
assetfinder --subs-only hackerone.com > assetfinder.txt
```

**Screenshot:**

<p align="center">
  <img src="https://github.com/DOLLY1552005/SKill_Horizon_Internship/blob/main/Subdomain_Enumeration/screenshots/assetfinder02.png" width="80%">
</p>

**Notes:**

* Found extra subdomains missed by Subfinder.
* Helped expand the coverage before generating permutations.

---

## 3. AlterX + dnsx

**Commands Used:**

```bash
cat subfinder.txt assetfinder.txt | alterx -p '{{sub}}-{{word}}.{{suffix}}' -o alterx_permutations.txt
cat alterx_permutations.txt | dnsx -o live_subdomains.txt
```


**Screenshot:**

<p align="center">
  <img src="https://github.com/DOLLY1552005/SKill_Horizon_Internship/blob/main/Subdomain_Enumeration/screenshots/alterx02.png" width="80%">
</p>

**Notes:**

* AlterX successfully generated permutations of discovered subdomains.
* However, dnsx did not find any of these permutations to be live.
* This is common in reconnaissance — it just means no extra valid subdomains were discovered through permutations for this target.

---

## Summary

* Combining three tools increased coverage of subdomains.
* dnsx filtered live subdomains → no new live subdomains found from permutations.
* The same methodology can be reused for any domain.

---
