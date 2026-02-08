# Affiliate Sembako Platform

Lightweight affiliate platform for basic-goods products, designed with **traffic-based fairness**, **anti-spam mechanics**, and **soft moderation**.

This project demonstrates backend system design focused on resource control, organic growth, and deterministic ranking — without heavy infrastructure.

---

## 🚀 Features

- **Affiliate Upload System**
  - Product uploads require quota
  - Prevents spam and low-quality flooding

- **Traffic-Based Reward**
  - Unique visitors generate upload quota
  - Repeated clicks are ignored

- **Deterministic Product Ranking**
  - Based on price, rating, and sales
  - Optional promotion credit (lightweight boost)

- **Soft Moderation (Report System)**
  - Weighted reports from affiliates and viewers
  - Content visibility decreases gradually

- **Cron Auto-Promotion**
  - Inactive affiliates lose influence over time
  - No hard delete, no sudden reset

---

## 🧠 Design Principles

- **Upload is a cost, not a right**  
  Affiliates must bring real traffic to earn uploads.

- **Organic traffic > click spam**  
  Only unique daily visitors are counted.

- **Bad content sinks naturally**  
  Moderation affects ranking, not instant deletion.

- **Inactive accounts do not block the system**  
  Resources are slowly recycled via cron jobs.

---

## 🗂 Project Structure

