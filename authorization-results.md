# 🔐 Authorization Testing Results – Booking System (Phase 3)

Author: Maria Kalu  
Date: 5/4/2025  
Environment: Kali Linux + Docker

---

## ✅ Summary Table – Page Access per User Role

| Page / Feature               | Guest | Reserver | Admin | Notes |
|-----------------------------|--------|----------|--------|-------|
| `/` (Home)                  | ✅     | ✅       | ✅     | All users can access |
| View resource list          | ✅     | ✅       | ✅     | Available on homepage |
| View resource form          | ❌     | ✅       | ✅     | Guests blocked from interacting |
| Create new resource         | ❌     | ❌       | ✅     | Admin-only |
| `/login`                    | ✅     | ✅       | ✅     | Login page open to all |
| `/register`                 | ✅     | ✅       | ✅     | Registration page open to all |
| `/resources`                | ❌     | ✅       | ✅     | Protected page |
| `/reservation`              | ❌     | ✅       | ✅     | Protected route |
| `/profile`                  | ❌     | ✅       | ✅     | Users only see their own |
| `/admin/users`              | ❌     | ❌       | ✅     | Admin dashboard |
| `/admin/settings`           | ❌     | ❌       | ✅     | Hidden from UI but accessible directly |
| `/api/reservations/:id`     | ❌     | ⚠️       | ✅     | Reserver can access others’ data (Horizontal Escalation) |
| `/api/users/:id`            | ❌     | ⚠️       | ✅     | Reserver can view another user's data |
| Hidden endpoints (wfuzz)    | ⚠️     | ⚠️       | ✅     | Discovered via fuzzing |

---

## 🧪 ZAP Scan Summary

- **Scan Tool**: OWASP ZAP (via proxy 127.0.0.1:8080)
- **Scan Users**: Guest, Reserver, Admin

### 🔍 Key Findings:
- Reflected input on reservation POST endpoint
- No CSRF token missing alerts (protection implemented)
- Admin endpoints well hidden from UI, but still accessible
- Some API endpoints lack proper role checks

### 📄 ZAP Report:
_Saved in this repo as `zap_report.md`._

---

## 🌐 Fuzzing Results (wfuzz + httpie)

### Commands Used:

```bash
# Find general pages
wfuzz -c -w /usr/share/wordlists/dirb/common.txt --hc 404 http://localhost:8080/FUZZ

# Find API endpoints
wfuzz -c -w /usr/share/wordlists/dirb/common.txt --hc 404 http://localhost:8080/api/FUZZ

# Discover reservation IDs
wfuzz -c -z range,1-1000 --hc 404 http://localhost:8080/api/reservations/FUZZ

# Fetch reservation data
http http://localhost:8080/api/reservations/1
