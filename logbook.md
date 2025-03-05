
# Logbook

| Date       | Used Hours | Subject(s)          | Output            |
|------------|------------|---------------------|-------------------|
| 30.10.2024 | 2          | Kick-off lecture    | Lecture recording |
| 31.10.2024 | 2          | Kick-off lecture    | Lecture recording |
| 01.11.2024 | 3          | Design discussion   | Wireframes draft  |
| 02.11.2024 | 4          | Coding: Login page  | Functional login  |



# Logbook - Booking System Phase 1

## 1. Initial Setup
- Cloned the repository:
  ```bash
  git clone https://github.com/vheikkiniemi/animated-waddle.git
  cd animated-waddle/Booking\ system/Phase\ 1/Ver2


## 2. Built and ran the database:


docker compose -f 'docker-compose.yml' up -d --build 'database'
Built and ran the web interface:


docker compose -f 'docker-compose.yml' up -d --build 'web'
