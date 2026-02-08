---
layout: persian  # یا single با کلاس rtl-layout
classes: wide rtl-layout
dir: rtl
title: "Cross-Entropy"
permalink: /teaching/studenteffort/toolkit/CrossEntropy/
author_profile: false
sidebar:
  nav: "toolkit"
header:
  overlay_image: "/assets/images/background.jpg"
  overlay_filter: 0.3
  overlay_color: "#5e616c"
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
---



# به‌روزرسانی پارامترهای نرون سیگمویدی با Cross-Entropy

مدل نرون:

$$
\hat y = g(z) = \sigma(z) = \sigma(w^T x + b)
$$

که در آن:

- $x$ بردار ویژگی‌ها
- $w$ وزن‌ها
- $b$ بایاس
- $z = w^T x + b$
- $\sigma(z) = \frac{1}{1+e^{-z}}$

مسئله: طبقه‌بندی دودویی

---

# تابع ضرر Cross-Entropy دودویی

برای یک نمونه با برچسب واقعی $y \in \{0,1\}$:

$$
L = -\big[y \log(\hat y) + (1-y)\log(1-\hat y)\big]
$$

---

# هدف یادگیری

$$
\min_{w,b} L
$$

با گرادیان کاهشی:

$$
w \leftarrow w - \eta \frac{\partial L}{\partial w}
$$

$$
b \leftarrow b - \eta \frac{\partial L}{\partial b}
$$

---

# محاسبه گرادیان — مرحله به مرحله

## مشتق loss نسبت به خروجی

$$
\frac{\partial L}{\partial \hat y}
=
-\left(\frac{y}{\hat y} - \frac{1-y}{1-\hat y}\right)
$$

---

## مشتق سیگموید

$$
\frac{d\sigma}{dz} = \sigma(z)(1-\sigma(z)) = \hat y(1-\hat y)
$$

---

## نتیجه مهم (ساده‌سازی بزرگ)

با قاعده زنجیره:

$$
\frac{\partial L}{\partial z}
=
\hat y - y
$$

این ساده شدن دلیل اصلی استفاده Cross-Entropy با سیگموید است.

---

# گرادیان نسبت به وزن‌ها

چون:

$$
z = w^T x + b
$$

داریم:

$$
\frac{\partial z}{\partial w} = x
$$

پس:

$$
\frac{\partial L}{\partial w}
=
(\hat y - y) x
$$

---

# گرادیان نسبت به بایاس

$$
\frac{\partial L}{\partial b}
=
\hat y - y
$$

---

# قانون به‌روزرسانی پارامترها

## وزن‌ها:

$$
w \leftarrow w - \eta (\hat y - y)x
$$

## بایاس:

$$
b \leftarrow b - \eta (\hat y - y)
$$

---

# تفسیر شهودی

ترم خطا:

$$
(\hat y - y)
$$

- اگر $\hat y > y$ → بیش‌برآورد → وزن‌ها کاهش
- اگر $\hat y < y$ → کم‌برآورد → وزن‌ها افزایش

---

# فرم برداری برای یک Batch

اگر $X$ ماتریس داده باشد:

$$
\nabla_w L = X^T(\hat y - y)
$$

---

# الگوریتم خلاصه

