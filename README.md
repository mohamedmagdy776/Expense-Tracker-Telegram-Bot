# 💸 Expense Tracker Telegram Bot

An intelligent automation workflow built with n8n that transforms Telegram messages (text or voice) into structured expense data and logs them directly into Google Sheets.

---

## 🚀 Overview

This workflow allows users to send expense details via Telegram in natural language (or voice), and automatically converts them into clean, structured data including:

* Price
* Item
* Place (merchant)
* Date
* Number of items
* Currency

The processed data is then appended to a Google Sheet for tracking and analysis.

---

## ⚙️ Workflow Structure

The workflow operates in the following sequence:

1. **Telegram Trigger**

   * Listens for incoming messages (text or voice).

2. **Switch Node**

   * Determines whether the input is:

     * Text message
     * Voice message

3. **Voice Path (if applicable)**

   * **Get File**: Downloads the voice message
   * **Transcribe Recording**: Converts speech to text

4. **Edit Fields**

   * Prepares and standardizes the input for the AI Agent

5. **AI Agent**

   * Processes the message using a structured system prompt
   * Extracts relevant expense data
   * Outputs clean JSON

6. **Code (JavaScript)**

   * Optional formatting or validation of the extracted data

7. **Google Sheets (Append Row)**

   * Stores the structured expense into the spreadsheet

---

## ✨ Features

* 📩 Accepts both **text and voice inputs** via Telegram
* 🧠 Uses AI to extract structured financial data
* 📊 Automatically logs expenses into Google Sheets
* 🌍 Supports relative dates ("today", "yesterday", etc.)
* 💱 Handles multiple currencies with normalization
* ⚡ Fully automated workflow (no manual input needed)

---

## 🤖 AI Agent Importance

The AI Agent is the core of this system.

Instead of relying on rigid parsing rules, the AI Agent:

* Understands **natural language** (Arabic & English supported)
* Extracts key entities even from messy or incomplete input
* Handles different sentence structures and formats
* Converts human input into **consistent structured JSON**

This makes the system highly flexible and scalable compared to traditional rule-based approaches.

---

## 🧠 AI Agent System Prompt

The AI Agent is guided by a strict system prompt that ensures reliable output.

### Key Responsibilities:

* Extract:

  * Merchant (place)
  * Price
  * Item
  * Quantity
  * Date
  * Currency

* Enforce:

  * Output must be **valid JSON only**
  * Missing values should be `null`

* Handle Dates:

  * Convert relative dates like:

    * "today"
    * "yesterday"
    * "day before yesterday"
  * Into exact format: `YYYY-MM-DD`

* Normalize Currency:

  * Defaults to EGP if not specified
  * Detects USD, EUR, SAR, etc.

---

## 📦 Output Structure

Example output from the AI Agent:

```json
{
  "expense_details": {
    "merchant": "Pizza Hut",
    "price": "400 EGP",
    "item": "Pizza",
    "quantity": 1,
    "date": "2026-01-25",
    "currency": "EGP"
  },
  "original_query": "اشتريت بيتزا من بيتزا هت النهاردة بـ 400 جنيه"
}
```

---

## 📊 Google Sheets Integration

Each processed expense is automatically appended to a sheet with columns like:

* price
* item
* place
* date
* currency
* number of items

---

## 🔁 Example Flow

**User Input (Telegram):**

> "اشتريت موبايل من Tradeline بـ 40000 امبارح"

**System Output:**

* Item: Mobile Phone
* Place: Tradeline
* Price: 40000 EGP
* Date: (yesterday → resolved date)
* Quantity: 1

---

## 🧩 Summary

This project demonstrates how to:

* Convert **unstructured user input (text/voice)**
* Into **clean, structured financial data**
* Using an AI-powered automation workflow

It is ideal for building personal finance trackers, business expense logs, or conversational data pipelines.

---

## 📌 Notes

* Designed for extensibility (can integrate with dashboards, databases, etc.)
* Can be adapted for other domains beyond expenses
* Works seamlessly with multilingual inputs

👨‍💻 Author
Eng. Mohamed Magdy Elghandour
AI Automation Engineer 🚀
